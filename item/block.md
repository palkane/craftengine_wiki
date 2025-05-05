# 🧱 方块物品  
方块物品是指绑定到特定方块的物品。您可在此配置对应的方块ID，或完整的方块配置（需注意：此举会使方块加载时间计入物品加载流程）。将此行为绑定至物品后，可通过右键点击放置对应方块。

⚠️ 注意：方块的放置位置取决于其 🕹️ 方块行为。例如图示中的树苗只能放置在带有`dirt`（泥土）或`farmland`（耕地）标签的方块上，因其方块行为遵循树苗特性。

```yaml
items:
  default:palm_sapling:
    material: paper
    behavior:
      type: block_item
      block: default:palm_sapling
```

这是配置方块物品的最简方式，前提是您已预先配置目标方块。若需了解方块配置方法，请参阅 🧱 方块 章节。

若分开配置过于繁琐，可采用合并配置方案。下方示例中，`block` 节点遵循标准方块配置格式：

```yaml
items:
  default:palm_sapling:
    material: paper
    custom-model-data: 1005
    settings:
      fuel-time: 100  # 燃烧时长（刻）
    data:
      item-name: "<!i><i18n:item.palm_sapling>"  # 本地化名称键
    model:
      template: "default:model/generated"  # 使用生成模型模板
      arguments:
        model: "minecraft:item/custom/palm_sapling"  # 物品模型路径
        texture: "minecraft:block/custom/palm_sapling"  # 纹理路径
    behavior:
      type: block_item
      block:
        settings:
          template: "default:settings/sapling"  # 继承树苗预设
          overrides:
            item: default:palm_sapling  # 覆盖关联物品
        behavior:
          type: sapling_block  # 方块类型：树苗
          feature: craftengine:palm_tree  # 生成树种
          bone-meal-success-chance: 0.45  # 骨粉催熟概率
          tags:  # 允许放置的基底标签
            - minecraft:dirt
            - minecraft:farmland
            - minecraft:sand
        loot:  # 掉落物配置
          template: "default:loot_table/basic"
          arguments:
            item: default:palm_sapling
        states:  # 方块状态
          properties:
            stage:  # 生长阶段属性
              type: int
              default-value: 0
              range: 0~1
          appearances:  # 外观配置
            default:
              state: oak_sapling:0  # 引用橡树苗状态
              model:
                path: "minecraft:block/custom/palm_sapling"
                generation:
                  parent: "minecraft:block/cross"  # 十字交叉模型
                  textures:
                    "cross": "minecraft:block/custom/palm_sapling"
          variants:  # 状态变体
            stage=0:
              appearance: "default"
              id: 0
            stage=1:
              appearance: "default"
              id: 1
```