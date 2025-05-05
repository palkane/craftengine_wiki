### 📄 模板系统使用指南 [必读]  
本文主要讲解如何在服务器中添加新模板。  

---  

### 简介  
本插件拥有极高的可定制性，但若完全不提供配置则无法运行。即使是最简短的选项也需要在YAML文件中声明一行。当此类选项数量庞大时，配置文件会变得冗长复杂。为此，插件引入了**模板系统**——您可以通过定义基础模板，结合参数填充（`arguments`）和覆盖项（`overrides`）来动态修改部分参数，从而大幅简化配置流程，减少重复工作量。下文将通过示例帮助您快速掌握模板系统的运作方式。  

---  

### 如何创建模板？  

#### 创建基础模板  
在YAML文件中以 `templates` 作为根键声明模板：  
```yaml
templates:
  namespace:template_id:  # 模板唯一标识符
    option_1: true        # 自定义配置项
    option_2: false  
    option_3: 
      - "hello"
    option_4: 20.25
```  
- `namespace:template_id` 是模板的唯一ID，在其他地方调用时必须使用此名称。  
- 模板下的配置区域完全自定义，只需遵守YAML语法即可。  

#### 创建含参数的模板  
若需动态参数，可用 `{ }` 包裹占位符：  
```yaml
templates:
  namespace:template_id:
    option_1: "{value_1}"  # 参数化配置
    option_2: "{value_2}"
    option_3:
      - "{value_3}"
    option_4: "{value_4}"
```  

---  

### 如何应用模板？  

#### 应用基础模板  
假设配置物品 `test:item_1`，无模板时的写法：  
```yaml
items:
  test:item_1:
    option_1: true
    option_2: false
    option_3: 
      - "hello"
    option_4: 20.25
```  
使用模板后的等效写法：  
```yaml
items:
  test:item_1:
    template: namespace:template_id  # 直接引用模板
```  
> 模板类似于预配置的"盒子"，调用时会自动展开其内容到当前配置区域。  

⚠️ **禁止**在同一个配置块中混用模板和普通配置！正确做法是使用 `overrides`：  
```yaml
# ❌ 错误示例
items:
  invalid:item:
    template: invalid:template
    option_1: a  # 非法混合配置

# ✅ 正确示例
items:
  invalid:item:
    template: invalid:template
    overrides:
      option_1: a  # 通过覆盖项修改
      option_2: c
```  

#### 应用含参数的模板  
通过 `arguments` 为模板占位符赋值：  
```yaml
items:
  test:item_1:
    template: namespace:template_id
    arguments:
      value_1: true      # 直接赋值
      value_2: false
      value_3: "hello"
      value_4: 20.25
```  
> 除直接赋值外，插件还支持自动递增ID等高级参数类型，详见 🟢 [参数类型文档]。  

#### 应用含覆盖项的模板  
若需新增或修改模板未定义的选项，使用 `overrides`：  
```yaml
items:
  test:item_1:
    template: namespace:template_id
    overrides:
      option_1: false    # 覆盖原模板值（true→false）
      missing_option: 2025  # 新增原模板没有的选项
```  
> `overrides` 不受参数类型限制，可自由定义复杂结构：  
```yaml
overrides:
  map:
    a: b
  list:
    - 1
    - 2
```  

#### 应用多模板组合  
支持通过数组组合多个模板（类似Rust的trait组合模式）：  
```yaml
templates:
  namespace:template_1:
    option_1: true
  namespace:template_2:
    option_2: false

items:
  test:item_1:
    template:
      - namespace:template_1  # 合并模板1
      - namespace:template_2  # 合并模板2
```  
> 若多个模板存在相同选项，**后声明的模板会覆盖前者**：  
```yaml
# 配置
templates:
  namespace:template_1:
    option_1: true
  namespace:template_2:
    option_1: false  # 最终生效值

# 结果
items:
  test:item_1:
    option_1: false
```  

#### 完整功能整合示例  
**配置：**  
```yaml
templates:
  namespace:template_1:
    option_1: true
    option_3: "{value}"
  namespace:template_2:
    option_2: false

items:
  test:item_1:
    template:
      - namespace:template_1  # 组合模板
      - namespace:template_2
    arguments:
      value: 2025            # 参数填充
    overrides:
      option_4:              # 覆盖新增
        - "hello"
```  

**等效结果：**  
```yaml
items:
  test:item_1:
    option_1: true     # 来自template_1
    option_2: false    # 来自template_2
    option_3: 2025     # 参数填充结果
    option_4:          # 覆盖新增项
      - "hello"
```