# 物品
完整的物品配置包含以下部分：  

**material（必填）**  

material（材料）作为物品的基础模板，例如paper（纸）或wooden_sword（木剑）。  

**custom-model-data（可选）**  

custom-model-data（自定义模型数据）是一个正整数，相同材料的自定义物品应具有不同的custom-model-data值。该数值决定了物品显示的模型，对下方的模型章节至关重要。

物品配置示例：  
```yaml
items:
  default:topaz_rod:
    material: fishing_rod  # 基础物品类型：钓鱼竿
    custom-model-data: 1000  # 自定义模型数据值（需唯一）
    data:
      display-name: "<!i><#FF8C00>黄晶钓竿"  # 显示名称（橙色粗体）
    model:
      template: models:fishing_rod_2d  # 使用2D钓竿模型模板
      arguments:  # 模型参数
        rod_model: minecraft:item/custom/topaz_rod  # 钓竿模型路径
        rod_texture: minecraft:item/custom/topaz_rod  # 钓竿贴图路径
        rod_cast_model: minecraft:item/custom/topaz_rod_cast  # 抛竿状态模型路径
        rod_cast_texture: minecraft:item/custom/topaz_rod_cast  # 抛竿状态贴图路径
```

### item-model（1.21.2+ 可选配置）  
定义该物品的模型资源路径。例如：`default:custom_book`  

版本适配说明：  
- 1.21.4+ 路径格式：`assets/[命名空间]/items/`  
- 1.21.2+ 路径格式：`assets/[命名空间]/models/item/`  

配置示例：  
```yaml
items:
  default:topaz_rod:
    material: fishing_rod  # 基础物品类型：钓鱼竿
    item-model: minecraft:topaz_rod  # 直接指定模型资源路径
    data:
      display-name: "<!i><#FF8C00>黄晶钓竿"  # 显示名称（橙色粗体）
    model:
      template: models:fishing_rod_2d  # 使用2D钓竿模型模板
      arguments:  # 模型参数（同上）
        rod_model: minecraft:item/custom/topaz_rod
        rod_texture: minecraft:item/custom/topaz_rod
        rod_cast_model: minecraft:item/custom/topaz_rod_cast
        rod_cast_texture: minecraft:item/custom/topaz_rod_cast
```
---------------------------------------------------------------

使用 **custom-model-data** 具有更好的版本兼容性，因为它自 **1.14** 版本起就已支持，而 **item-model** 至少需要 **1.21.2** 版本。  

你可以同时使用 **custom-model-data** 和 **item-model**。  

------------------------------------------------------

在配置 **model** 部分时，必须指定 **custom-model-data** 或 **item-model** 中的一项。  
- 如果你的资源包支持 **1.21.2** 或更高版本，插件会自动使用物品 ID 作为 **item-model** 的值。  
- 但如果你的物品 ID 包含不符合 Minecraft 命名规则的字符，可能导致资源包无法正常加载。  
- 在这种情况下，你必须改用 **custom-model-data**，或手动指定一个合法的 **item-model** 值。

--------------------------------------------------------------

### **配置项说明（可选）**  

#### **data（可选）**  
📊 **[物品数据](item/itemdata.md)**  

#### **behavior（可选）**  
🎮 **[物品行为](item/behaviors.md)**  

#### **settings（可选）**  
⚙️ **[物品设置](item/itemsetting.md)**  

#### **model（可选）**  
🟰 **[物品模型](item/model.md)**  

#### **category（可选）** 查看`提示`界面  
📂 **分类**  

---

### **完整配置示例**  
```yaml
items:
  default:palm_log:  # 物品ID：棕榈木
    material: paper  # 基础材质：纸
    custom-model-data: 1000  # 自定义模型数据
    settings:  # 物品设置
      fuel-time: 300  # 燃烧时间（300刻 = 15秒）
      tags:  # 物品标签
        - "default:palm_logs"  # 属于“棕榈木”分类
        - "minecraft:logs"  # 属于原木类
        - "minecraft:logs_that_burn"  # 属于可燃原木
    data:
      display-name: "<!i>棕榈木"  # 显示名称（斜体）
    model:  # 模型配置
      type: "minecraft:model"  # 模型类型
      path: "minecraft:item/custom/palm_log"  # 模型路径
      generation:  # 模型生成规则
        parent: "minecraft:block/custom/palm_log"  # 继承方块模型
    behavior:  # 物品行为
      type: block_item  # 类型：方块物品
      block: default:palm_log  # 对应方块ID
```

### **关键说明**
- **`custom-model-data`** 用于兼容 **1.14+** 版本，确保自定义物品模型正确显示。  
- **`settings`** 可定义物品的燃烧时间、标签等实用属性。  
- **`model`** 部分支持引用自定义模型，并支持从方块模型继承（如 `parent` 设定）。  
- **`behavior`** 定义物品的交互逻辑，例如 `block_item` 表示该物品可放置为对应方块。  

> **提示**：若物品ID包含非法字符（如大写字母或特殊符号），建议使用 **`custom-model-data`** 或手动指定合法的 **`item-model`**，以避免资源包加载错误。