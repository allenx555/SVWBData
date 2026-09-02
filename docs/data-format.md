# 数据格式

## 通用结构

三份数据均为 UTF-8 JSON。顶层对象只有一个与文件名相同的表名；表名下按语言代码分组，
每个语言对象再把文本 ID 映射到字符串。

```json
{
  "cardnametext": {
    "Chs": {
      "CN_000000000": "示例名称"
    }
  }
}
```

字符串可以为空。读取端必须保留原始换行、空格和标记，不应在载入时主动去除格式。

## 文件与 ID

| 文件 | 顶层表名 | 常见 ID | 用途 |
|---|---|---|---|
| `cardnametext.json` | `cardnametext` | `CN_<数字>` | 卡牌及相关对象名称 |
| `cardtext.json` | `cardtext` | `Card_<数字>` | 卡牌界面通用文本 |
| `skilldesctext.json` | `skilldesctext` | `SD_<数字>_<序号>` | 技能与效果描述 |

这些 ID 是文本键，不应直接假定为运行时卡牌 ID。若要和主数据关联，应由使用方在本地
完成显式映射。

## 语言代码

| 代码 | 语言 |
|---|---|
| `Jpn` | 日语 |
| `Eng` | 英语 |
| `Chs` | 简体中文 |
| `Kor` | 韩语 |
| `Cht` | 繁体中文 |
| `Fre` | 法语 |
| `Ita` | 意大利语 |
| `Ger` | 德语 |
| `Spa` | 西班牙语 |

`cardnametext` 和 `skilldesctext` 当前包含全部九种语言；`cardtext` 当前只包含
`Jpn`、`Chs`、`Kor`、`Cht`。

## 内嵌标记

技能文本可能包含颜色、下划线、注音、动态占位符和条件显示标记。这些标记属于原始
文本数据的一部分。展示层可以在副本上解析或清理，但仓库快照应原样保存，以免破坏
语义或后续校对能力。

机器读取时应遵循 [`schemas/localized-text-table.schema.json`](../schemas/localized-text-table.schema.json)。

## 卡牌短码名称映射

`data/cards/hash-id-name-map.json` 保存主数据短码到基础卡牌和简体中文名称的映射：

```json
{
  "hash_id": "e4Gg",
  "base_card_id": "10503210",
  "name_keys": ["CN_10503210"],
  "name": "大游戏世界"
}
```

`hash_id` 来自 `CardMaster.HashId`，当前长度为 4 或 5，字符范围为字母、数字、下划线
和连字符。名称通过以下关系取得：

```text
CardMaster.HashId
  → CardMaster.CardTextId
  → CardText._Name
  → MasterTextLabel.Id
  → MasterTextLabel.Text
```

同一卡牌的普通、闪卡等变体会共享短码。映射按短码去重；若多个名称键最终显示同一个
名称，则全部保留在 `name_keys`。当前有 43 条主数据记录没有简体中文名称，使用
`name: null` 明确表示未解析，而不是删除短码。

机器读取时应遵循 [`schemas/hash-id-name-map.schema.json`](../schemas/hash-id-name-map.schema.json)。
