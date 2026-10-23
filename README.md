# 海外 APP 信息流广告多语种翻译 Skill

**app-ad-multilingual-translator · V1.0.0**

将中文海外 APP 广告脚本翻译为目标市场的标准通用口语，自动完成建议断句，交付逐行语义对齐的双语字幕表。保留中文原文，支持多脚本、多语言和定向修改；具备文件工具时，可读取 Word、Excel、CSV 并导出批量 Excel。

Faithful multilingual translation and bilingual subtitle segmentation for Chinese mobile-app ads. No dedicated translation API or API key required.

## 下载

- [下载可导入的 Skill ZIP](https://github.com/Lip-smacking/app-ad-multilingual-translator/raw/refs/heads/main/downloads/app-ad-multilingual-translator.zip)
- [查看核心指令](SKILL.md)
- [查看原始 V1.0 Prompt](references/original-prompt.md)

ZIP 内仅包含一个 `app-ad-multilingual-translator/` 目录，`SKILL.md` 位于该目录根部。不要把 GitHub 自动下载的整个源码仓库包与专用 Skill 导入包混淆。

## 安装与兼容

沿用“蓝胖子”的标准 `SKILL.md` 和 ZIP 分发方式，面向 Codex、Claude Code、Cursor、WorkBuddy、豆包工作等客户端。是否支持技能导入、自动触发和附件处理，以客户端当前版本及权限为准；本项目不声称已在上述所有客户端完成实机验证。

**Codex 本地安装：** 将 ZIP 解压后，把 `app-ad-multilingual-translator` 文件夹放入本机的 `~/.codex/skills/`；使用其他技能目录配置时，放入配置的目录。

也可用 Git 克隆到技能目录（目标目录应不存在）：

```bash
git clone https://github.com/Lip-smacking/app-ad-multilingual-translator.git ~/.codex/skills/app-ad-multilingual-translator
```

**Claude Code、Cursor：** 将同名技能文件夹放入该客户端配置的 skills 目录，按其技能发现方式启用。

**WorkBuddy、豆包工作：** 如果当前版本提供“上传技能”或“导入技能”入口，上传上面的专用 ZIP 并启用。没有入口时，可将 [SKILL.md](SKILL.md) 内容粘贴到对话中，再附上待翻译脚本；这是单次提示词使用，不能视为持久安装。

## 使用示例

```text
使用海外 APP 广告多语种翻译：
目标：英语（美国）、葡萄牙语（巴西）
脚本001：剪视频太麻烦？用这个APP，剪辑更轻松。现在就试试！
保留中文原文，按建议断句逐行双语对照。
```

支持显式技能调用的客户端也可使用：

```text
$app-ad-multilingual-translator 将附件脚本翻译为英语（美国）和葡萄牙语（巴西），导出 Excel。
```

指定修改时可说：“仅修改脚本003的巴西葡语第2个意群，其他内容保持不变。”

## 输出规则

- 少量脚本：每个脚本、每个市场各一张双列表格，中文在左、目标语在右。
- 批量脚本：每种语言/市场一个 Excel 工作表，A列中文、B列译文、C列脚本ID、D列断句序号，另保留“原始脚本”表。
- 中文断句直接拼接后与原文逐字符相同；不改写广告信息、不转换币种、不增减优惠条件。
- 没有音视频与时间信息时输出“建议断句”，不提供虚构时间轴；有关键歧义时单列待确认。

## 工具与依赖

与蓝胖子一样，不绑定专用 MCP 或固定工具白名单。Skill 只提供工作指令，不自带翻译引擎，不会授予账户或系统权限。

| 场景 | 宿主需要提供的能力 |
|---|---|
| 粘贴文本翻译与双语表格 | 普通模型对话 |
| Word / Excel / CSV 输入 | 已授权的文件读取或文档、表格工具 |
| 批量 `.xlsx` 交付 | 文件写入与表格导出工具，或可用的本地代码环境 |
| 官方名称、术语核实 | 可选的搜索或浏览器能力 |

普通翻译无需联网，无需专用 API key。缺少文件工具时如实说明，并提供可复制表格、TSV 或 JSON；不伪造 Excel 下载链接。

## 目录

```text
SKILL.md
agents/openai.yaml
references/file-delivery.md
references/original-prompt.md
README.md
LICENSE
downloads/app-ad-multilingual-translator.zip
```

## 作者与许可

作者：Haiyannnn（GitHub：[@Lip-smacking](https://github.com/Lip-smacking)）。采用 [MIT License](LICENSE)，允许个人与商业使用、修改和再发布，需保留版权及许可声明。
