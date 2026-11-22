---
date: 2026-11-23
topic: 规范
status: active
---

# 团队读写规范（usage）

## 写入
- **唯一通道**：GitHub Contents API
  `PUT https://api.github.com/repos/uuuu33ii/team-memory/contents/{path}`
  Header: `Authorization: Bearer <token>`，body 含 `message`、`content`（base64）、`sha`（更新已有文件时必填，先 GET 获取）
- 禁用 `git push` 直连（本环境到 github.com 的 git 端点不稳定）
- 大文件（>1MB）改用 Releases 或 Gist

## 读取（按优先级）
1. **jsDelivr（公开仓库，国内直连快）**：`https://cdn.jsdelivr.net/gh/uuuu33ii/team-memory@main/{path}` — 注意缓存延迟（约 5 分钟~数小时），适合读不急于最新的内容
2. **raw.githubusercontent.com**：`https://raw.githubusercontent.com/uuuu33ii/team-memory/main/{path}` — 本环境实测不稳定，仅备选
3. **Gist raw**：`https://gist.githubusercontent.com/{user}/{gist_id}/raw/{file}` — 单文件轻量、无缓存，适合高频更新的小型热数据（如当前任务状态）
4. **API 兜底**：`GET /repos/uuuu33ii/team-memory/contents/{path}`（base64），最可靠但最慢

## 命名与格式
- topics 文件：`topics/<kebab-case-name>.md`，必须带元数据头（见 template.md）
- 数据文件：`data/<kebab-case-name>.json`
- 交付物索引：`deliverables/` 下只放索引 md，不放交付物本体
- 每次新增/修改记忆，必须同步更新 `INDEX.md`
