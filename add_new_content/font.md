### ㊙️ 字体配置指南  
本页说明如何添加新字体  

---

#### **TTF字体**  
[![Minecraft Wiki](https://minecraft.wiki/favicon.ico)](https://minecraft.wiki/w/Font)  
需在以下路径创建`default.json`文件（若已存在则直接追加配置）：  
```json
// default.json
{
    "providers": [
        {
            "type": "ttf",
            "file": "minecraft:custom_font.ttf",  // TTF文件路径
            "oversample": 10,  // 抗锯齿采样率
            "size": 11         // 基础字号
        }
    ]
}
```

---

#### **位图字体**  
[![Minecraft Wiki](https://minecraft.wiki/favicon.ico)](https://minecraft.wiki/w/Font)  
替换原版字符图像只需将PNG文件放入指定路径即可  

---

#### **UniHex字体（罕见用途）**  
[![Minecraft Wiki](https://minecraft.wiki/favicon.ico)](https://minecraft.wiki/w/Font)  
```json
{
    "providers": [
        {
            "type": "unihex",
            "hex_file": "minecraft:font/unifont_jp.zip",
            "size_overrides": [
                {
                    "__ranges": [
                        "Enclosed CJK Letters and Months",
                        "CJK Compatibility",
                        "CJK Unified Ideographs Extension A",
                        "Yijing Hexagram Symbols",
                        "CJK Unified Ideographs"
                    ],
                    "from": "\u3200",
                    "to": "\u9FFF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "CJK Compatibility Ideographs"
                    ],
                    "from": "\uF900",
                    "to": "\uFAFF",
                    "left": 0,
                    "right": 15
                }
            ],
            "filter": {
                "jp": true
            }
        },
        {
            "type": "unihex",
            "hex_file": "minecraft:font/unifont.zip",
            "size_overrides": [
                {
                    "__ranges": [
                        "CJK Symbols and Punctuation",
                        "Hiragana",
                        "Katakana"
                    ],
                    "from": "\u3001",
                    "to": "\u30FF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Enclosed CJK Letters and Months",
                        "CJK Compatibility",
                        "CJK Unified Ideographs Extension A",
                        "Yijing Hexagram Symbols",
                        "CJK Unified Ideographs"
                    ],
                    "from": "\u3200",
                    "to": "\u9FFF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Hangul Jamo"
                    ],
                    "from": "\u1100",
                    "to": "\u11FF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Hangul Compatibility Jamo"
                    ],
                    "from": "\u3130",
                    "to": "\u318F",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Hangul Jamo Extended-A"
                    ],
                    "from": "\uA960",
                    "to": "\uA97F",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Hangul Jamo Extended-B"
                    ],
                    "from": "\uD7B0",
                    "to": "\uD7FF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Hangul Syllables",
                    ],
                    "from": "\uAC00",
                    "to": "\uD7AF",
                    "left": 1,
                    "right": 15
                },
                {
                    "__ranges": [
                        "CJK Compatibility Ideographs"
                    ],
                    "from": "\uF900",
                    "to": "\uFAFF",
                    "left": 0,
                    "right": 15
                },
                {
                    "__ranges": [
                        "Halfwidth and Fullwidth Forms"
                    ],
                    "from": "\uFF01",
                    "to": "\uFF5E",
                    "left": 0,
                    "right": 15
                }
            ]
        }
    ]
}
```  
> 注：此配置涉及CJK字符集的多语言精细控制，建议参考Wiki调整范围参数