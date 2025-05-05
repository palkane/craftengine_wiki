# ✅ **选择（Select）**  
https://minecraft.wiki/w/Items_model_definition#select  

根据离散属性渲染物品模型。  

使用 `"minecraft:select"` 时，需要指定一个属性类型：  
- `cases` 表示匹配不同情况的模型列表  
- `fallback` 表示未找到有效匹配时使用的备用模型（可选参数，若未提供则会渲染为 `"missing"` 错误模型）  

**代码示例：**  
```yaml
items:
  default:select_item:
    model:
      type: "minecraft:select"
      property: "minecraft:charge_type"  # 指定属性类型
      cases:
        - when: arrow  # 当属性值为"arrow"时
          model:
            type: minecraft:model
            path: "minecraft:item/custom/model_1"
        - when: rocket  # 当属性值为"rocket"时
          model:
            type: minecraft:model
            path: "minecraft:item/custom/model_2"
      fallback:  # 默认模型
        type: minecraft:model
        path: "minecraft:item/custom/model_3"
```

### **可用属性**  
1. **`minecraft:charge_type`**  
   返回 `minecraft:charged_projectiles` 组件中存储的投射物装填类型（如箭、烟花火箭等）。  

2. **`minecraft:context_dimension`**  
   返回当前渲染上下文所在的维度ID（若存在）。  

3. **`minecraft:context_entity_type`**  
   返回持有该物品的实体类型（若存在）。  

4. **`minecraft:display_context`**  
   返回物品当前的渲染上下文（如手持、地面掉落、物品栏等）。

5. **`minecraft:main_hand`**  
   返回持有该物品的玩家主手（`left` 或 `right`）。  

6. **`minecraft:trim_material`**  
   返回物品的 `minecraft:trim` 组件中 `material` 字段的值（若存在）。  

7. **`minecraft:block_state`**  
   返回物品的 `minecraft:block_state` 组件中指定方块属性的值。  

   **代码示例：**  
   ```yaml
   type: "minecraft:select"
   property: "minecraft:block_state"
   block-state-property: "facing"  # 获取方块的朝向属性
   ```

8. **`minecraft:component`**  
   返回指定组件的值。若该值来自注册表但当前数据包未提供，则静默忽略该条目。  

   **代码示例：**  
   ```yaml
   type: "minecraft:select"
   property: "minecraft:component"
   component: "minecraft:unbreakable"  # 检测物品是否不可破坏
   ```

9. **`minecraft:custom_model_data`**  
   返回物品的 `minecraft:custom_model_data` 组件中指定索引的字符串值。  

   **代码示例：**  
   ```yaml
   type: "minecraft:select"
   property: "minecraft:custom_model_data"
   index: 0  # 读取索引0处的字符串值
   ```

10. **`minecraft:local_time`**  
    返回根据指定格式（`pattern`）格式化的当前时间（每秒更新）。支持本地化（`locale`）和时区（`time-zone`），完整格式规则请参考 **ICU（Unicode国际化组件）** 文档。  

    **代码示例：**  
    ```yaml
    type: "minecraft:select"
    property: "minecraft:local_time"
    locale: "en_US"        # 使用美式英语格式
    time-zone: "GMT+0:45"  # 指定时区（GMT+0:45）
    pattern: "HH:mm:ss"    # 时间格式（24小时制时分秒）
    ```  
