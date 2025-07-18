---
{
    "title": "SHOW-ALTER",
    "language": "zh-CN"
}

---

## SHOW-ALTER

### Name

SHOW ALTER

## 描述

该语句用于展示当前正在进行的各类修改任务的执行情况

```sql
SHOW ALTER [CLUSTER | TABLE [COLUMN | ROLLUP] [FROM db_name]];
```

说明：

1. TABLE COLUMN：展示修改列的 ALTER 任务
2. 支持语法[WHERE TableName|CreateTime|FinishTime|State] [ORDER BY] [LIMIT]
3. TABLE ROLLUP：展示创建或删除 ROLLUP index 的任务
4. 如果不指定 db_name，使用当前默认 db
5. CLUSTER: 展示集群操作相关任务情况（仅管理员使用！待实现...）

## 举例

1. 展示默认 db 的所有修改列的任务执行情况

   ```sql
   SHOW ALTER TABLE COLUMN;
   ```

2. 展示某个表最近一次修改列的任务执行情况

   ```sql
   SHOW ALTER TABLE COLUMN WHERE TableName = "table1" ORDER BY CreateTime DESC LIMIT 1;
   ```

3. 展示指定 db 的创建或删除 ROLLUP index 的任务执行情况

   ```sql
   SHOW ALTER TABLE ROLLUP FROM example_db;
   ```

4. 展示集群操作相关任务（仅管理员使用！待实现...）

   ```
   SHOW ALTER CLUSTER;
   ```

### Keywords

    SHOW, ALTER

### Best Practice
