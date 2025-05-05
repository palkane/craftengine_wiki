# 📐 模型配置  
（参考链接：https://minecraft.wiki/w/Items_model_definition#model）

模型由两个核心部分组成：路径（path）和着色（tints）。其中着色为可选配置，所有可用的着色类型可通过下方链接查看。

[🎨 着色应用示例](item/tint.md)  
在此配置中，我们为自定义棕榈树叶创建模型。由于原版树叶默认不带颜色，需通过着色配置实现染色效果：

![](picture/model/piaxe.png)

```yaml
default:palm_leaves:
  model:
    type: "minecraft:model"  # 标准模型类型
    path: "minecraft:item/custom/palm_leaves"  # 模型资源路径
    generation:
      parent: "minecraft:block/custom/palm_leaves"  # 继承方块模型基础
    tints:  # 着色配置组
      - type: "minecraft:constant"  # 固定值着色类型
        value: -12012264  # 十六进制颜色码（ARGB格式）
```

技术说明：
1. `-12012264`对应#F4A460的ARGB编码（沙棕色）
2. 着色系统支持动态生物群系染色（如`minecraft:foliage`类型）
3. 当同时定义多个着色层时，将按声明顺序叠加效果