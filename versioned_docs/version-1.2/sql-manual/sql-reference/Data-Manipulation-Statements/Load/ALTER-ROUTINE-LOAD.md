---
{
    "title": "ALTER-ROUTINE-LOAD",
    "language": "en"
}
---

## ALTER-ROUTINE-LOAD

### Name

ALTER ROUTINE LOAD

### Description

This syntax is used to modify an already created routine import job.

Only jobs in the PAUSED state can be modified.

grammar:

```sql
ALTER ROUTINE LOAD FOR [db.]job_name
[job_properties]
FROM data_source
[data_source_properties]
```

1. `[db.]job_name`

   Specifies the job name to modify.

2. `tbl_name`

   Specifies the name of the table to be imported.

3. `job_properties`

   Specifies the job parameters that need to be modified. Currently, only the modification of the following parameters is supported:

   1. `desired_concurrent_number`
   2. `max_error_number`
   3. `max_batch_interval`
   4. `max_batch_rows`
   5. `max_batch_size`
   6. `jsonpaths`
   7. `json_root`
   8. `strip_outer_array`
   9. `strict_mode`
   10. `timezone`
   11. `num_as_string`
   12. `fuzzy_parse`


4. `data_source`

   The type of data source. Currently supports:

   KAFKA

5. `data_source_properties`

   Relevant properties of the data source. Currently only supports:

   1. `kafka_partitions`
   2. `kafka_offsets`
   3. `kafka_broker_list`
   4. `kafka_topic`
   5. Custom properties, such as `property.group.id`

   Note:

   1. `kafka_partitions` and `kafka_offsets` are used to modify the offset of the kafka partition to be consumed, only the currently consumed partition can be modified. Cannot add partition.

### Example

1. Change `desired_concurrent_number` to 1

   ```sql
   ALTER ROUTINE LOAD FOR db1.label1
   PROPERTIES
   (
       "desired_concurrent_number" = "1"
   );
   ```

2. Modify `desired_concurrent_number` to 10, modify the offset of the partition, and modify the group id.

   ```sql
   ALTER ROUTINE LOAD FOR db1.label1
   PROPERTIES
   (
       "desired_concurrent_number" = "10"
   )
   FROM kafka
   (
       "kafka_partitions" = "0, 1, 2",
       "kafka_offsets" = "100, 200, 100",
       "property.group.id" = "new_group"
   );
   ```

### Keywords

    ALTER, ROUTINE, LOAD

### Best Practice

