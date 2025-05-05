### 🏭️ 模型生成系统  
本文主要讲解如何使用模型生成功能。  

---  

#### **配置位置**  
如果您仔细观察，会发现插件在多个地方使用以下配置格式：  
```yaml
path: "xxx"  # 模型路径
generation:  # 模型生成配置
  parent: "minecraft:xxx/xxx"  # 父模型
  textures:  # 纹理覆盖
    "xxx": "xxx"
```  

实际上，**所有支持`path`参数的地方**（即需要指定模型路径的配置项），都可以使用`generation`来动态生成模型。  

- 如果您已手动创建了JSON模型文件并放入`resourcepack`目录，只需填写`path`即可直接引用。  
- 如果没有现成模型文件，但希望插件基于父模型自动生成，则应使用`generation`配置。  

---  

#### **参数说明**  
当前`generation`支持两个核心参数：  

1. **parent** (父模型)  
   - 可引用Minecraft原版模型（如`minecraft:block/cube_all`）  
   - 也可指向自定义模型路径  
   - 📜 [所有可用Minecraft原版模型参考](https://misode.github.io/assets/model/)  

2. **textures** (纹理覆盖)  
   - 用于替换父模型中定义的纹理变量  

---  

#### **配置示例**  
以下是一个完整方块模型的生成配置：  
```yaml
generation:
  parent: "minecraft:block/cube_all"  # 使用MC的全方位方块模板
  textures:
    "particle": "minecraft:block/custom/block_particle"  # 粒子效果纹理
    "down": "minecraft:block/custom/block_down"         # 底面纹理
    "up": "minecraft:block/custom/block_up"             # 顶面纹理
    "north": "minecraft:block/custom/block_north"       # 北面纹理
    "east": "minecraft:block/custom/block_east"         # 东面纹理
    "south": "minecraft:block/custom/block_south"       # 南面纹理
    "west": "minecraft:block/custom/block_west"         # 西面纹理
```  
> 插件会根据此配置自动生成符合`cube_all`模型的JSON文件，并替换所有指定面的纹理。  

---  

#### **注意事项**  
1. 纹理路径需遵循Minecraft资源包规范  
2. 若父模型本身有嵌套引用（如`cube_all`引用了`block`模板），纹理变量名必须与父模型定义严格一致  
3. 生成后的模型文件会输出到资源包对应路径，可通过`path`字段覆盖默认生成位置  

通过此系统，您无需手动编写重复的JSON模型文件即可快速创建标准化模型！