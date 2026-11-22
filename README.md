# Team Memory — 团队持久化记忆仓库

> 元数据头规范：每条记忆文件必须以如下 YAML 头开始：
> ```yaml
> ---
> date: YYYY-MM-DD
> topic: <主题，如 逆向情报 / 方案结论 / 能力盘点>
> status: active | superseded | archived
> ---
> ```

## 目录结构
- `INDEX.md` — 记忆索引：每条记忆一行（文件路径 + 一句话摘要 + 日期）
- `topics/` — 按主题存放知识文档（逆向情报、方案结论、能力盘点规范等）
- `data/` — 结构化数据（json，如基线哈希、抓取结果）
- `deliverables/` — 交付物索引（记录交付物名称、位置、日期）
- `usage.md` — 团队读写规范

## 写入/读取通道约定
- **写入（唯一通道）**：`api.github.com`（PUT /repos/uuuu33ii/team-memory/contents/{path}，Bearer token），禁用 git push 直连（网络不稳定）
- **读取**：首选 `https://cdn.jsdelivr.net/gh/uuuu33ii/team-memory@main/{path}`（注意 5 分钟~数小时缓存）；raw.githubusercontent.com 本环境不稳定，仅作备选

## 新增一条记忆的步骤
1. 在 `topics/`（或 `data/`、`deliverables/`）创建带元数据头的文件
2. 在 `INDEX.md` 追加一行索引
3. 一次提交（contents API 可多文件分批，但 INDEX 更新放在同一批次）

仓库地址：https://github.com/uuuu33ii/team-memory
