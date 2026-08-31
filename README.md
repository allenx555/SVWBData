# SVWBData

SVWBData 是一个面向研究、互操作与自动化开发的卡牌文本数据快照仓库。仓库只保存
规范化后的多语言文本 JSON，以及解释数据格式、更新流程和验证要求的文档。

## 仓库内容

```text
data/texts/extracted/
├─ cardnametext.json
├─ cardtext.json
└─ skilldesctext.json

docs/
├─ data-format.md
├─ extraction-process.md
├─ verification.md
└─ maa-integration.md

schemas/
├─ localized-text-table.schema.json
└─ manifest.schema.json
```

当前快照包含：

- Android 包名：`com.netease.yzs`
- APK 版本：`11.9.0`（`versionCode 200`）
- Unity 版本：`2022.3.62f2`

| 文件 | 语言数 | 每种语言条目数 |
|---|---:|---:|
| `cardnametext.json` | 9 | 5,356 |
| `cardtext.json` | 4 | 300 |
| `skilldesctext.json` | 9 | 9,442 |

文件哈希、字节数和各语言条目数见 [`manifest.json`](manifest.json)。数据结构见
[`docs/data-format.md`](docs/data-format.md)，更新与验证要求见
[`docs/extraction-process.md`](docs/extraction-process.md) 和
[`docs/verification.md`](docs/verification.md)。

## 明确不收录的内容

本仓库不包含 APK、AssetBundle、解密后的 UnityFS、卡图、模拟器截图、主数据库、
反编译产物、分析日志、账号数据、解包程序、第三方工具或依赖环境。公开文档也不披露
资源保护密钥、私有偏移或可直接复用的完整解密实现。

## 权利说明

本仓库与游戏开发商、发行商及相关权利方无隶属或背书关系。游戏名称、卡牌名称、技能
文本及其翻译的权利归各自权利方所有；本仓库不对这些提取文本授予许可证。仓库自有的
说明文档也不改变原始游戏数据的权利归属。

若公开分发这些文本不符合你所在地的法律、服务条款或权利方要求，请不要继续分发。
权利方可通过仓库的问题追踪渠道提出更正或移除请求。

由于数据部分不由仓库维护者拥有，本仓库暂不附加覆盖全部内容的开源许可证。
