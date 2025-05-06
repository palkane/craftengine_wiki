# 🌎️ 客户端语言 (lang)  
```yaml
lang:  
  en_us:  
    item.custom.palm_leaves: Palm leaves 
    item.custom.palm_log: Palm log

```

若未配置语言文件，Minecraft将默认使用en_us（美式英语）。因此，若您正在创建新的翻译键，强烈建议至少配置en_us语言项。  

如需实现客户端翻译渲染，请插入以下格式说明：  
https://docs.advntr.dev/minimessage/format.html#translatable  

查阅Minecraft Wiki了解客户端翻译机制：  
https://minecraft.wiki/w/Resource_pack#Language  

如需覆盖所有语言版本（强制全局生效），请使用"all"标识符  

```yaml

lang:  
  all:  
    container.inventory: ""  

```