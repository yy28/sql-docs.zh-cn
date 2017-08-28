---
title: "PolyBase 故障排除 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: fa59193fcedb1d5437d8df14035fadca2b3a28f1
ms.openlocfilehash: e65ea926f3a2d2fb3c30c511a1fbba6150de7b42
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="polybase-troubleshooting"></a>PolyBase 故障排除
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要对 PolyBase 进行故障排除，请使用本主题中介绍的技术。  
  
## <a name="catalog-views"></a>目录视图  
 使用此处列出的目录视图来管理 PolyBase 操作。  
  
|||  
|-|-|  
|视图|说明|  
|[sys.external_tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|标识外部表。|  
|[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|标识外部数据源。|  
|[sys.external_file_formats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|标识外部文件格式。|  
  
## <a name="dynamic-management-views"></a>动态管理视图  
  
|||  
|-|-|  
|[sys.dm_exec_compute_node_errors (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  
  
  PolyBase 查询拆分为 sys.dm_exec_distributed_request_steps 中的一系列步骤。 下表提供了从步骤名称到关联的 DMV 的映射。
  
 |PolyBase 步骤|关联的 DMV|  
 |-|-| 
 |HadoopJobOperation | sys.dm_exec_external_operations|
 |RandomIdOperation | sys.dm_exec_distributed_request_steps|
 |HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
 |StreamingReturnOperation | sys.dm_exec_dms_workers|
 |OnOperation | sys.dm_exec_distributed_sql_requests |
  
  
## <a name="to-monitor-polybase-queries-using-dmvs"></a>使用 DMV 监视 PolyBase 查询  
 使用以下 DMV 对 PolyBase 查询进行监视和故障排除。  
  
1.  **查找运行时间最长的查询**  
  
     记录运行时间最长的查询的执行 ID。  
  
    ```tsql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **查找分布式查询运行时间最长的步骤**  
  
     使用上一步中记录的执行 ID。 记录运行时间最长的步骤的索引。  
  
     检查运行时间最长的步骤的 location_type：  
  
    -   头或计算：表示 SQL 操作。 继续执行步骤 3a。  
  
    -   DMS：表示 PolyBase 数据移动服务操作。 继续执行步骤 3b。  
  
    ```tsql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **查找运行时间最长的步骤的执行进度**  
  
    1.  **查找 SQL 步骤的执行进度**  
  
         使用上一步中记录的执行 ID 和步骤索引。 使用上一步中记录的执行 ID 和步骤索引。  
  
        ```tsql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **查找 DMS 步骤的执行进度**  
  
         使用上一步中记录的执行 ID 和步骤索引。  
  
        ```tsql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **查找有关外部 DMS 操作的详细信息**  
  
     使用上一步中记录的执行 ID 和步骤索引。  
  
    ```tsql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>查看 PolyBase 查询计划  
  
1.  在 SSMS 中，启用“包含实际的执行计划”(Ctrl+M)，并运行查询。  
  
2.  单击“执行计划”  选项卡。  
  
     ![PolyBase 查询计划](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase 查询计划")  
  
3.  右键单击“远程查询运算符”，然后选择“属性”。  
  
4.  将远程查询值复制并粘贴到文本编辑器中，以查看 XML 远程查询计划。  以下是一个示例。  
  
    ```xml  
  
    <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
           [T1_1].[CustomerKey] AS [CustomerKey],  
           [T1_1].[GeographyKey] AS [GeographyKey],  
           [T1_1].[Speed] AS [Speed],  
           [T1_1].[YearMeasured] AS [YearMeasured]  
    FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                   [T2_1].[CustomerKey] AS [CustomerKey],  
                   [T2_1].[GeographyKey] AS [GeographyKey],  
                   [T2_1].[Speed] AS [Speed],  
                   [T2_1].[YearMeasured] AS [YearMeasured]  
            FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
            WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
    </dsql_query>  
    ```  
  
## <a name="to-monitor-nodes-in-a-polybase-group"></a>在 PolyBase 组中监视节点  
 在将一组计算机配置为 PolyBase 扩展组的一部分后，便可以监视计算机的状态。 有关创建扩展组的详细信息，请参阅 [PolyBase 扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
  
1.  连接到组的头节点上的 SQL Server。  
  
2.  运行 DMV [sys.dm_exec_compute_nodes (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) 以查看 PolyBase 组中的所有节点。  
  
3.  运行 DMV [sys.dm_exec_compute_node_status (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) 以查看 PolyBase 组中的所有节点的状态。  
  
 ## <a name="known-limitations"></a>已知的限制
 
 PolyBase 具有以下限制： 
 - 最大行大小（包括可变长度列的全长）不能超过 1 MB。 
 - PolyBase 不支持 Hive 0.12+ 数据类型（即 Char()、VarChar()）   
 - 将数据从 SQL Server 或 Azure SQL 数据仓库导出为 ORC 文件格式时，由于 Java 内存不足错误，包含大量文本的列可能会被限制为 50 列。 若要解决此问题，请仅导出列的一个子集。
- [向 SQL Server 2016 故障转移群集添加节点时，PolyBase 没有安装](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)
  
## <a name="error-messages-and-possible-solutions"></a>错误消息和可能的解决方案

有关解决外部表的错误，请参阅 Murshed Zaman 的博客 [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase 安装错误和可能的解决方案")。

## <a name="see-also"></a>另请参阅
[PolyBase Kerberos 连接疑难解答](polybase-troubleshoot-connectivity.md)

