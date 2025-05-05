### 🪑 家具系统  
本文主要讲解如何在服务器中添加新家具。  

⚠️ **重要提示**  
重载插件**不会影响已放置的家具**！必须重启服务器或重新加载区块才能使现有家具应用新配置。插件使用缓存优化家具性能，强制重载已加载的家具可能严重影响服务器稳定性。未来可能会加入不安全的重载标志，但目前不支持。  

---

### **配置模块**  
完整家具配置包含以下部分：  
- 🕹️ [家具行为(未完成)]  


- ⚙️ [家具设置](furniture/fumiture_setting.md)  


- 📍 [家具放置方式](furniture/furniture_placement.md)  


- 💎 [战利品系统(未完成)]

#### **🪑 家具物品绑定**  
```yaml
furniture:
  default:bench:  # 家具ID
    settings:
      item: default:bench  # 绑定的物品ID
      sounds:
        break: minecraft:block.bamboo_wood.break  # 破坏音效
        place: minecraft:block.bamboo_wood.place  # 放置音效
```

---

### **完整配置示例**  
```yaml
furniture:
  default:bench:
    settings: {...}
    placement:
      ground:  # 地面放置配置
        rules:
          rotation: EIGHT     # 旋转精度: ANY/FOUR/EIGHT/SIXTEEN/NORTH/EAST/WEST/SOUTH
          alignment: CENTER  # 对齐方式: ANY/CENTER/HALF/QUARTER/CORNER
        elements:
          - item: default:bench  # 显示物品
            display-transform: NONE  # 变形模式
            billboard: FIXED        # 广告牌模式
            position: 0.5,0,0       # 相对位置
            translation: 0,0.5,0    # 位移补偿
        hitboxes:  # 碰撞箱
          - position: 0,0,0    # 坐标
            width: 1            # 宽度
            height: 1           # 高度
            interactive: true   # 可交互
            seats:              # 座位坐标
              - "0,0,-0.1 0"   # 坐标+朝向
          - position: 1,0,0
            width: 1
            height: 1
            interactive: true
            seats:
              - "1,0,-0.1 0"
    loot:
      template: loot_table:normal  # 战利品表模板
      arguments:
        item: default:bench        # 掉落物
```

---

### **关键参数说明**  
1. **放置规则 (placement)**  
   - `rotation`: 支持8方向旋转  
   - `alignment`: 强制中心对齐  

2. **碰撞箱 (hitboxes)**  
   - 每个箱体可定义独立座位点  
   - 坐标格式: `"X,Y,Z 朝向"`  

3. **战利品 (loot)**  
   - 使用预定义战利品表模板  
   - 支持参数化掉落物配置  

> 注：所有位置坐标均为相对值（基于家具原点）