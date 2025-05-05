### 📖 合成配方系统  
本文主要讲解如何在服务器中添加新配方。

---

#### **兼容其他插件的物品**  
要在CraftEngine中使用其他插件的物品参与合成：

1. **创建匹配物品条目**  
   在CraftEngine中注册一个与外部插件物品外观（纹理/模型）完全相同的物品。

2. **使用注册ID**  
   所有配方必须使用CraftEngine注册的物品ID。

3. **兼容性要求**  
   外部插件需满足以下条件之一：
   - 官方支持与CraftEngine兼容，或
   - 支持通过NBT标签/组件存储CraftEngine标识符

**配置示例（以CustomFishing为例）**：
```yaml
# 1.20-1.20.4版本
nbt:
  craftengine:id: namespace:value
# 1.20.5+版本
components:
  minecraft:custom_data:
    craftengine:id: namespace:value
```

---

#### **配方配置结构**  
所有配方配置必须位于YAML根节点的`recipes`项下。

#### **标签系统**  
支持使用原版标签和自定义标签，格式为`#namespace:tag`。  
示例为棕榈木板添加两个原版标签：
```yaml
items:
  default:palm_planks:
    material: paper
    custom-model-data: 1004
    settings:
      fuel-time: 300
      tags:
        - "minecraft:planks"              # 原版木板标签
        - "minecraft:wooden_tool_materials" # 原版木质工具材料标签
    # ...其他配置...
```

---

### **配方分类系统**

#### **分组与类别**  
```yaml
recipes:
  default:palm_planks:
    type: shapeless
    category: building  # 配方书标签页（固定选项）
    group: planks       # 客户端解锁分组（自定义名称）
    ingredients:
      A: "#default:palm_logs"
    result:
      id: default:palm_planks
      count: 4
```

**类别选项**：  
- 烹饪类：`food`/`blocks`/`misc`  
- 合成类：`building`/`redstone`/`equipment`/`misc`

---

### **配方类型详解**

#### **有序合成（Shaped）**  
```yaml
default:topaz_shovel:
  type: shaped
  pattern:    # 合成图案
    - "A"
    - "B"
    - "B"
  ingredients:
    A: "default:topaz"
    B: "minecraft:stick"
  result:
    id: default:topaz_shovel
    count: 1
```

#### **无序合成（Shapeless）**  
```yaml
default:palm_planks:
  type: shapeless
  ingredients:
    - "#default:palm_logs"  # 支持标签
    - - test:ingredient1    # 支持备选材料列表
      - test:ingredient2
  result:
    id: default:palm_planks
    count: 4
```

#### **烹饪类配方**  
支持`smelting`/`blasting`/`smoking`/`campfire_cooking`类型：
```yaml
default:topaz_from_smelting_topaz_ore:
  type: smelting
  experience: 1.0    # 获得经验值
  cookingtime: 200   # 熔炼耗时（刻）
  ingredient: "default:topaz_ore"
  result:
    id: default:topaz
    count: 1
```

#### **切石机配方**  
⚠️ 不建议使用自定义物品作为原料（可能导致客户端显示异常）：
```yaml
default:stonecutting_example:
  type: stonecutting
  ingredient: "minecraft:stone"
  result:
    id: default:topaz
    count: 1
```

#### **锻造台配方**  
```yaml
default:topaz_bow:
  type: smithing_transform
  template-type: default:topaz  # 模板槽位（可选）
  base: minecraft:bow           # 基础物品（必需）
  addition: default:topaz       # 附加材料（可选）
  merge-components: true        # 是否合并组件（默认true）
  post-processors: []           # 后处理配置
  result:
    id: default:topaz_bow
    count: 1
```

**自定义后处理器**示例：
```yaml
post-processors:
  # 保留指定组件（1.20.5+）
  - type: keep_components
    components:
      - minecraft:enchantments
  # 保留指定NBT标签（1.20-1.20.4）
  - type: keep_tags
    tags:
      - display.Name
      - CustomModelData
```