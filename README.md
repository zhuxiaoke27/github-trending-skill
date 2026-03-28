# GitHub Trending Skill

一个用于 OpenClaw 的 GitHub 趋势分析技能，支持获取热门项目、趋势对比和生成报告。

## 功能特性

### 📊 基础功能
- 获取 GitHub Trending 项目（每日/每周/每月）
- 按编程语言过滤
- 自定义返回数量（1-15 个项目）
- 深度分析项目（提取 README 和功能说明）

### 🔄 趋势对比
- 对比不同时间段的趋势变化
- 识别新上榜项目、持续热门项目
- 分析热度变化趋势

### 📝 报告生成
- **周报**：采样 3 天数据，生成本周 Top 10 + 技术趋势
- **月报**：采样 2-3 周数据，生成月度趋势分析
- 包含热门语言统计、领域趋势、特别推荐

## 使用方法

### 基础查询
```bash
# 获取今日热门项目（默认前 10 个）
github trending

# 获取本周热门项目
github trending -p weekly

# 获取本月热门项目，返回前 5 个
github trending -p monthly -l 5

# 按语言过滤（如 Python）
github trending -L python
```

### 趋势对比
```bash
# 对比今日和本周趋势
github trending --compare daily,weekly

# 对比本周和本月趋势
github trending --compare weekly,monthly
```

### 报告生成
```bash
# 生成本周报告
github trending --report weekly-report

# 生成月度报告
github trending --report monthly-report

# 生成 Python 项目月报
github trending --report monthly-report --language python
```

## 安装

### 方式 1：通过 ClawHub 安装（推荐）
```bash
clawhub install github-trending
```

### 方式 2：手动安装
```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/zhuxiaoke27/github-trending-skill.git github-trending
```

## 技能参数

| 参数 | 简写 | 说明 | 默认值 |
|------|------|------|--------|
| `--period` | `-p` | 时间段（daily/weekly/monthly） | daily |
| `--limit` | `-l` | 返回项目数量（1-15） | 10 |
| `--language` | `-L` | 按编程语言过滤 | 无 |
| `--compare` | 无 | 对比模式（如 daily,weekly） | 无 |
| `--report` | 无 | 报告模式（weekly-report/monthly-report） | 无 |

## 输出示例

### 基础查询输出
```
# GitHub Trending - Daily (2026-03-28)

## 1. owner/repo-name ⭐ 12,345 (+1,234 today)
**语言**: Python

项目描述和功能说明...

🔗 https://github.com/owner/repo-name
```

### 对比模式输出
```
# GitHub Trending 对比分析

## 📈 新上榜项目（仅在 weekly 出现）
- owner/new-repo

## 🔥 持续热门（同时出现在 daily 和 weekly）
- owner/hot-repo

## 📊 热度变化分析
...
```

### 报告模式输出
```
# GitHub 月度趋势报告（2026年3月）

## 🏆 Top 10 热门项目
...

## 📊 技术趋势分析
- 热门编程语言
- 核心趋势
- 特别关注项目
```

## 工作原理

1. **抓取 Trending 页面**：使用 `web_fetch` 获取 GitHub Trending 页面
2. **解析项目列表**：提取项目名称、Star 数、语言等信息
3. **深度分析**：访问每个项目页面，提取 README 内容
4. **智能处理**：
   - 去重（同一项目多次出现只统计一次）
   - 热度权重（基于出现频次）
   - 可选缓存（避免重复请求）

## 技术栈

- OpenClaw Skills Framework
- `web_fetch` 工具（获取网页内容）
- Markdown 解析
- JSON 数据缓存

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

MIT License

## 作者

[@zhuxiaoke27](https://github.com/zhuxiaoke27)

## 相关链接

- [OpenClaw 文档](https://docs.openclaw.ai)
- [ClawHub](https://clawhub.com)
- [GitHub Trending](https://github.com/trending)
