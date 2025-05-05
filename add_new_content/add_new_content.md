### **➕ 新增内容管理**  
本页面主要说明如何管理自定义内容。  

#### **📁 资源文件结构**  
在插件的根目录（`plugins/CraftEngine/resources/`）下，所有资源包均存储于此，**包名称可自定义**。每个资源包包含 **两个文件夹** 和 **一个 YAML 文件**：  
- **`configuration`**：存放配置文件  
- **`resourcepack`**：存放资源包文件（如材质、模型等）  
- **`pack.yml`**：存储资源包的元数据  

#### **📂 目录示例**  
```plaintext
plugins
  └ CraftEngine
     └ resources
         ├ pack_1          # 资源包1（自定义名称）
         ├ pack_2          # 资源包2
         └ pack_3          # 资源包3
            ├ configuration  # 配置文件夹
            ├ resourcepack   # 资源包文件夹
            └ pack.yml      # 资源包元数据文件
```  


# 元数据文件（Meta File）  
元数据文件是一个记录基础信息的YAML文档。其中最重要的条目是**命名空间（namespace）**。  

示例：  
```yaml
author: XiaoMoMi
version: 0.0.1
description: CraftEngine 默认资源包
namespace: default
enable: true # 设为 `false` 可禁用此资源包
```  

命名空间的作用范围仅限于YAML层级中根节点下的二级节点。例如，以下两种写法是等价的：  

显式指定命名空间：  
```yaml
blocks:
  default:palm_leaves:
    behavior:
      type: leaves_block
```  

隐式使用包命名空间（若未显式指定，则默认使用资源包中定义的命名空间）：  
```yaml
blocks:
  palm_leaves:
    behavior:
      type: leaves_block
```  

---  

### 配置目录结构  
配置文件的存储路径如下所示，支持`json`和`yml`格式。此外，您可以在`configuration`目录下自由创建子目录。  
```
plugins
  └ CraftEngine
     └ resources
         └ pack
            └ configuration
```  

在YAML配置中，**禁止**使用以下格式（同一配置项重复声明）：  
```yaml
items:
  default:topaz_helmet:
    template: default:topaz_armor
    arguments:
      part: helmet
      slot: head
items:
  default:topaz_boots:
    template: default:topaz_armor
    arguments:
      part: boots
      slot: feet
```  

需改为通过`#`添加标识符区分同名配置项，从而实现在单个YAML文件中定义多组同类型配置：  
```yaml
items#0:
  default:topaz_helmet:
    template: default:topaz_armor
    arguments:
      part: helmet
      slot: head
items#1:
  default:topaz_boots:
    template: default:topaz_armor
    arguments:
      part: boots
      slot: feet
```  

---  

### 资源包目录结构  
请确保资源包的目录结构如下所示，否则可能导致资源合并问题。其中`overlay_folder`、`pack.mcmeta`和`pack.png`为非必需文件。  
```
plugins
  └ CraftEngine
     └ resources
         └ pack
            └ resourcepack
               ├ assets
               ├ overlay_folder
               ├ pack.mcmeta
               └ pack.png
```