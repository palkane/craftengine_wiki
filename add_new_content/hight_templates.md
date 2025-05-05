### 🟢 参数类型说明  

#### 直接赋值（Direct Assignment）  
最简单的参数类型，直接为参数名赋予具体值：  
```yaml
arguments:
  value_1: true          # 布尔值
  value_2: 100           # 数值
  value_map:             # 映射表
    a: b
    c: d
  value_list:            # 列表
    - 123
    - 456
```  

⚠️ **重要限制**：  
直接赋值的映射表（map）内**禁止包含`type`字段**，否则会报错！此时应改用下文介绍的`map`类型参数。  
```yaml
# ❌ 错误示例（包含type字段）
value_map:
  type: c  # 非法字段
  a: b
  c: d

# ✅ 正确写法（改用map类型参数）
value_map:
  type: map  # 显式声明类型
  map:
    type: c  # 合法嵌套
    a: b
    c: d
```  

---  

### 需声明类型的参数  
所有非直接赋值的参数必须通过`type`字段指定类型。以下是支持的参数类型：  

#### 自增整数（self_increase_int）  
自动递增的数字ID，每次调用时数值+1。  

**配置示例**：  
```yaml
# 模板部分
variants:
  axis=x:
    appearance: axisX
    id: "{internal_id}"  # 占位符
  axis=y:
    appearance: axisY
    id: "{internal_id}"
  axis=z:
    appearance: axisZ
    id: "{internal_id}"

# 参数定义部分
arguments:
  internal_id:
    type: self_increase_int
    from: 0  # 起始值
    to: 2    # 结束值
```  

**等效结果**：  
```yaml
variants:
  axis=x:
    appearance: axisX
    id: 0  # 自动填充
  axis=y:
    appearance: axisY
    id: 1  # 递增值
  axis=z:
    appearance: axisZ
    id: 2  # 递增值
```  

---  

#### 映射表（map）  
用指定的映射表替换占位符。  

**正确用法**：  
```yaml
arguments:
  enchantments:
    type: map
    map:
      minecraft:sharpness: 1  # 完整的映射表定义
```  

⚠️ **使用限制**：  
映射表参数**必须完整替换占位符**，不可与其他内容拼接！  
```yaml
# ❌ 错误示例（尝试拼接）
template:
  components:enchantments: "{enchantments}, 123"  # 非法拼接

# ✅ 正确用法（完整替换）
template:
  components:enchantments: "{enchantments}"  # 完全替换为map内容
```  

---  

#### 列表（list）  
用指定的列表替换占位符。  

**配置示例**：  
```yaml
arguments:
  lore:
    type: list
    list:
      - "Hello, Minecraft!"  # 列表项
```  

⚠️ **使用限制**：  
列表参数同样**必须完整替换占位符**！  
```yaml
# ❌ 错误示例（尝试拼接）
template:
  lore: "{lore}, 1"  # 非法拼接

# ✅ 正确用法
template:
  lore: "{lore}"  # 完全替换为list内容
```  

---  

通过合理组合这些参数类型，您可以高效地实现动态化模板配置！