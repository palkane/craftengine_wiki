# 🎨 着色配置  
[参考文档](https://minecraft.wiki/w/Items_model_definition#Tint_sources_types)

所有颜色参数均支持十进制数值或RGB格式：

```yaml
# 十进制颜色值 (红色示例)
value: 16711680

# RGB数组格式
value:
  - 255
  - 0
  - 0

# RGB逗号分隔格式
value: 255,0,0
```

### 着色类型大全

1. **固定颜色**  
```yaml
type: "minecraft:constant"
value: -12012264  # 棕榈叶沙色
```

2. **自定义模型数据染色**  
```yaml
type: "minecraft:custom_model_data"
index: 0  # 模型数据索引
default: -12012264  # 默认颜色
```

3. **染料染色**  
```yaml
type: "minecraft:dye"
default: -12012264  # 基础颜色
```

4. **烟花染色**  
```yaml
type: "minecraft:firework"
default: -12012264  # 默认火花颜色
```

5. **生物群系草地染色**  
```yaml
type: "minecraft:grass"
temperature: 0.5  # 温度系数 (0.0-1.0)
downfall: 0.5  # 降水系数 (0.0-1.0)
```

6. **地图颜色**  
```yaml
type: "minecraft:map_color"
default: -12012264  # 地图显示颜色
```

7. **药水效果染色**  
```yaml
type: "minecraft:potion"
default: -12012264  # 药水基础色
```

8. **队伍染色**  
```yaml
type: "minecraft:team"
default: -12012264  # 队伍默认色
```