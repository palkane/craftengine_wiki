# ⚖️ 条件模型  
[官方文档](https://minecraft.wiki/w/Items_model_definition#condition)

当使用"minecraft:condition"时，需指定条件类型（即下方"property"参数）。"on-false"和"on-true"分别表示在不同条件下显示不同模型。

```yaml
items:
  default:condition_item:
    model:
      type: "minecraft:condition"  # 条件模型
      property: "minecraft:using_item"  # 条件检测类型
      on-false:  # 条件不满足时
        type: "minecraft:model"
        path: "minecraft:item/custom/model_false"  # 默认模型
      on-true:  # 条件满足时
        type: "minecraft:model"
        path: "minecraft:item/custom/model_true"  # 激活状态模型
```

### 可用条件属性

| 属性 | 说明 |
|------|------|
| `minecraft:broken` | 当物品可损坏且仅剩1次使用次数时返回true |
| `minecraft:carried` | 物品在GUI中被拖拽时返回true |
| `minecraft:damaged` | 当物品可损坏且至少被使用过1次时返回true |
| `minecraft:extended_view` | 按住Shift键查看物品详情时返回true（仅限UI界面） |
| `minecraft:fishing_rod/cast` | 钓鱼竿抛出浮标时返回true |
| `minecraft:selected` | 物品在快捷栏被选中时返回true |
| `minecraft:using_item` | 玩家正在使用该物品时返回true |
| `minecraft:view_entity` | 当观察的实体是本地玩家/旁观目标时返回true |
| `minecraft:bundle/has_selected_item` | 收纳袋在GUI中展开显示选中物品时返回true |

### 特殊条件类型

1. **组件检测**  
```yaml
type: "minecraft:condition"
property: "minecraft:has_component"
component: minecraft:enchantments  # 检测附魔组件
ignore-default: false  # 是否忽略默认组件
```

2. **按键检测**  
```yaml
type: "minecraft:condition"
property: "minecraft:keybind_down"
keybind: key.left  # 检测左方向键
```

3. **自定义模型数据**  
```yaml
type: "minecraft:condition"
property: "minecraft:custom_model_data"
index: 0  # 检测第0号自定义模型数据
```
