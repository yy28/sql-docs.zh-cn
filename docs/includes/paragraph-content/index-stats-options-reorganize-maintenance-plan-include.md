

### <a name="index-stats-options"></a>索引统计信息选项

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


在旧版 Microsoft SQL Server 中，可能会导致系统重新调整或重新生成大型索引，进而导致速度变慢。 SQL Server 2016 大幅提升了这些索引操作的性能。

此外，在旧版中，控制级别不太细致。 这导致系统重新调整或重新生成一些索引，即使这些索引的碎片百分比不高，也不例外。但这会造成资源浪费。 通过维护计划用户界面 (UI) 上的新版控件，可以根据索引统计信息条件来排除不需要刷新的索引。 为此，可以在内部使用下列 Transact-SQL 动态管理视图 (DMV)：


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **扫描类型**  
 系统必须使用资源才能收集索引统计信息。 可以选择使用相对较少还是较多的资源，具体取决于所需的索引统计信息精度。 UI 提供了以下精度级别列表，必须从中选择一个：


- Fast
- 抽样
- 详细


 **仅在以下情况下优化索引：**  
 UI 提供了以下可调筛选器，可用于避免刷新不是非常需要刷新的索引：


- 碎片 &gt; (%)
- 页计数 &gt;
- 用于过去（天）

