### 🔊 音效系统  
本页主要说明如何在服务器中添加新的音效  

---

#### **基础音效配置**  
```yaml
sounds:
  minecraft:custom_block.place:  # 音效事件ID
    replace: false  # 是否覆盖原版音效
    subtitle: "subtitles.custom_block.place"  # 字幕翻译键
    sounds:
      - "block/custom_block_1"  # 简单格式（自动补全路径）
  
  minecraft:custom_ambient.custom_biome:
    sounds:
      - name: "ambient/custom_biome_1"  # 详细格式
        volume: 0.4    # 音量（0.0-1.0）
        weight: 3      # 随机权重
      - name: "ambient/custom_biome_2"
        volume: 0.4
        weight: 7
      - name: "ambient/custom_biome_3"
        stream: false           # 是否流式加载
        attenuation-distance: 16  # 衰减距离
        preload: false          # 是否预加载
        type: "file"            # 文件类型
```

> 📘 **术语说明**  
> - **音效事件**：通过`/playsound`命令调用的标识符  
> - **实际音效**：存储在`sounds`列表中的音频文件  
> - 具体参数效果请参考 [Minecraft Wiki](https://minecraft.wiki/w/Sounds.json)  

---

#### **唱片机歌曲（1.21+）**  
⚠️ 需重启服务器才能生效（Minecraft注册机制限制）  
```yaml
jukebox_songs:
  default:credits_music:  # 歌曲ID
    sound: minecraft:music.credits  # 音效事件
    length: 100.0        # 时长（秒）
    description: "Credits"  # 显示名称  
    comparator-output: 15 # 红石比较器输出强度
    range: 32            # 播放范围
```

**关联物品示例**：  
```yaml
items:
  default:music_stick:
    material: stick
    data:
      jukebox-playable: default:credits_music  # 可播放的歌曲ID
```

> 💡 实时更新技巧：修改配置ID可实时注册新歌曲（无需重启）