# 🧩 复合模型  
[官方文档](https://minecraft.wiki/w/Items_model_definition#composite)

在同一个空间内渲染多个子模型，实现模型叠加效果。

```yaml
default:composite_item:
  model:
    type: "minecraft:composite"  # 复合模型类型
    models:  # 子模型列表（按渲染顺序排列）
      - type: minecraft:model
        path: "minecraft:item/custom/model_1"  # 底层模型
      - type: minecraft:model
        path: "minecraft:item/custom/model_2"  # 中层模型  
      - type: minecraft:model
        path: "minecraft:item/custom/model_3"  # 顶层模型
```
