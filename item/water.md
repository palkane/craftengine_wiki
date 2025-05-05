# 🌊 流体碰撞方块物品  
与普通方块物品（block_item）不同，流体碰撞方块物品会检测与流体的碰撞关系，适用于创建可放置在水面或岩浆表面的方块。其余配置选项与普通方块物品完全相同。

```yaml
items:
  default:reed:
    material: paper  # 基础材质
    behavior:
      type: liquid_collision_block_item  # 特殊行为类型
      offset-y: 1  # 方块的垂直放置偏移量（单位：格）
      block: default:reed  # 关联的方块ID
```
