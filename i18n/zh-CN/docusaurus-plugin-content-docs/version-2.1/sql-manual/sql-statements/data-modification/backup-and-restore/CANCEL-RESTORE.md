---
{
"title": "CANCEL RESTORE",
"language": "zh-CN"
}
---

## 描述

该语句用于取消一个正在进行的 RESTORE 任务。

## 语法

```sql
CANCEL RESTORE FROM <db_name>;
```

## 参数

**1.`<db_name>`**

恢复任务所属数据库名。

## 注意事项：

- 当取消处于 COMMIT 或之后阶段的恢复左右时，可能导致被恢复的表无法访问。此时只能通过再次执行恢复作业进行数据恢复。

## 示例

1. 取消 example_db 下的 RESTORE 任务。

```sql
CANCEL RESTORE FROM example_db;
```

