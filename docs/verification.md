# 发布前验证

每次快照更新必须同时通过结构、完整性与公开边界检查。

## JSON 结构

- 三个文件均能作为 UTF-8 JSON 完整解析。
- 每个文件只有一个预期顶层表名。
- 语言代码属于文档列出的九种代码。
- 每个语言表都是“文本 ID → 字符串”的映射。
- 允许空字符串，但不允许 `null`、数字、数组或嵌套对象作为文本值。
- 数据符合 `schemas/localized-text-table.schema.json`。

## 快照一致性

- 实际文件大小和 SHA-256 与 `manifest.json` 一致。
- 每种语言的条目数与清单一致。
- 同一数据表的各语言通常应拥有相同键集合；若不一致，必须在更新说明中解释。
- 更新差异中不应出现未经确认的大规模删除或整种语言清空。
- `manifest.json` 自身符合 `schemas/manifest.schema.json`。

## 公开边界

提交前检查 Git 跟踪文件，确保只有：

```text
.gitignore
README.md
manifest.json
data/texts/extracted/*.json
docs/**
schemas/**
```

同时搜索并排除：

- Windows、Linux 或 macOS 的本机绝对路径
- URL 中的访问令牌、认证头、Cookie、账号和设备标识
- 可执行文件、脚本、压缩包、二进制资源与图片
- 解密密钥、私有偏移、运行时注入步骤和完整解密代码

## 当前基线

当前快照共有 3 个 JSON、22 个语言表和 134,382 个本地化字符串槽位，其中允许包含
空字符串。详细分项与哈希以根目录 `manifest.json` 为准。
