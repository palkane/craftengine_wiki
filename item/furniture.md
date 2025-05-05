# 🪑 家具物品  

家具物品是指绑定到某件家具上的物品。您可以在此配置其对应的家具ID，甚至完整的家具配置（但请注意，这样做会导致加载家具所需的时间被计入物品加载流程）。当您将此行为绑定到物品后，可通过右键点击放置该家具。

```yaml
items:
  default:bench:
    behavior:
      type: furniture_item
      furniture: default:bench
```

这是配置家具物品的最简方式，但前提是您已预先配置好对应的家具。若不清楚如何配置家具，请查阅 [🪑 家具](furniture/fumiture.md) 章节。

若您认为分开配置过于繁琐，可选择合并配置。以下示例中，`furniture` 下的格式遵循标准家具配置规范。

```yaml
items:
  default:bench:
    material: paper
    custom-model-data: 2000
    data:
      display-name: "<!i>长椅"
    model:
      type: "minecraft:model"
      path: "minecraft:item/custom/bench"
    behavior:
      type: furniture_item
      furniture:
        settings:
          item: default:bench
          sounds:
            break: minecraft:block.bamboo_wood.break
            place: minecraft:block.bamboo_wood.place
        placement:
          ground:
            rules:
              rotation: EIGHT
              alignment: CENTER
            elements:
              - item: default:bench
                display-transform: NONE
                billboard: FIXED
                position: 0.5,0,0
                translation: 0,0.5,0
            hitboxes:
              - position: 0,0,0
                width: 1
                height: 1
                interactive: true
                seats:
                  - 0,0,-0.1 0
              - position: 1,0,0
                width: 1
                height: 1
                interactive: true
                seats:
                  - 1,0,-0.1 0
        loot:
          template: loot_table:normal
          arguments:
            item: default:bench
```