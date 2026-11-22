---
date: 2026-11-23
topic: 规范
status: active
---

# 记忆文件元数据头模板

每条记忆文件必须以如下 YAML 头开始，保证任何成员可快速检索：

```yaml
---
date: YYYY-MM-DD
topic: <主题枚举：逆向情报 | 方案结论 | 能力盘点 | 基线 | 规范>
status: active | superseded | archived
---
```

## 示例

```yaml
---
date: 2026-11-23
topic: 逆向情报
status: active
---
```

## 状态约定
- `active`：当前有效结论，可被引用
- `superseded`：已被新结论取代（需在新文件中注明取代它的文件路径）
- `archived`：仅存档，不再维护
