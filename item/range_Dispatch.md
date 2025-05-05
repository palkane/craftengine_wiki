# 📡 范围调度
https://minecraft.wiki/w/Items_model_definition#range_dispatch

根据数值属性渲染物品模型。系统会选择最后一个阈值小于或等于属性值的条目。

当使用"minecraft:range_dispatch"时，您需要指定数值属性类型。其中：  
- `scale` 表示属性值的乘数因子  
- `entries` 表示不同数值下对应的模型  
- `fallback` 表示未找到有效条目时的备用模型对象（可选参数，若未指定则会渲染为"missing"错误模型）

代码示例：
```yaml
items:
  default:range_dispatch_item:
    model:
      type: "minecraft:range_dispatch"
      property: "minecraft:crossbow/pull"
      entries:
        - model:
            type: minecraft:model
            path: "minecraft:item/custom/model_1"
          threshold: 0.58
        - model:
            type: minecraft:model
            path: "minecraft:item/custom/model_2"
          threshold: 1.0
      fallback:
        type: minecraft:model
        path: "minecraft:item/custom/model_3"
```

# 可用属性：  

- `minecraft:crossbow/pull`  
  返回弩的特定使用时间  

---

- `minecraft:bundle/fullness`  
  返回`minecraft:bundle_contents`组件的重量值，若不存在则返回0  

---

- `minecraft:cooldown`  
  返回物品剩余冷却时间，按比例缩放为0.0至1.0之间的值

---

- `minecraft:compass`  
返回持有者位置与目标点在X-Z平面上的夹角（按比例缩放为0.0至1.0）。若目标无效（不存在、位于其他维度或距离持有者过近）则返回随机值。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:compass"
target: spawn  # 目标点设为出生点
wobble: true   # 启用指针抖动效果
```

---

- `minecraft:count`  
返回物品堆叠数量。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:count"
normalize: true  # 将数值归一化处理
```

---

- `minecraft:damage`  
返回物品的`minecraft:damage`组件值，若不存在则返回0。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:damage"
normalize: true  # 将数值归一化处理
```

---

- `minecraft:time`  
返回游戏内时间（按比例缩放为0.0至1.0）。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:time"
source: daytime  # 时间源设为昼夜周期
wobble: true     # 启用时间波动效果
```

---

- `minecraft:use_cycle`  
返回物品使用进度的周期模数值（剩余使用刻数取模周期）。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:use_cycle"
period: 1.0  # 设定周期长度
```

---

- `minecraft:use_duration`  
返回物品已使用的游戏刻数。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:use_duration"
remaining: false  # 禁用剩余时间模式（返回已用时间而非剩余时间）
```

---

- `minecraft:custom_model_data`  
返回物品的`minecraft:custom_model_data`组件中指定索引的浮点数值，若不存在则返回0。  

代码示例：  
```yaml
type: "minecraft:range_dispatch"
property: "minecraft:custom_model_data"
index: 0  # 指定读取数据的索引位置
```