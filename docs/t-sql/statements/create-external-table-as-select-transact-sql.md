---
title: "创建外部 TABLE AS SELECT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CREATE EXTERNAL TABLE AS SELECT
- CREATE_EXTERNAL_TABLE_AS_SELECT
- CREATE EXTERNAL TABLE AS SELECT_TSQL
helpviewer_keywords:
- External, table
- PolyBase, external table
- External, table create as select
- PolyBase, create table as select
ms.assetid: 32dfe254-6df7-4437-bfd6-ca7d37557b0a
caps.latest.revision: "16"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f2ca379cf30fe2e7d359a294a18804f0b5e6faeb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-table-as-select-transact-sql"></a>创建外部 TABLE AS SELECT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  创建外部表，然后，在并行，将结果导出的[!INCLUDE[tsql](../../includes/tsql-md.md)]到 Hadoop 或 Azure 存储 Blob 的 SELECT 语句。  
  
 使用创建外部表 AS 选择 (CETAS) 语句：  
  
-   将数据库表导出到 Hadoop 或 Azure blob 存储。  
  
-   从 Hadoop 或 Azure blob 存储导入数据并将其存储在数据库中。  
  
-   从 Hadoop 或 Azure blob 存储查询数据、 将其联接使用数据库关系表，和将结果写回到 Hadoop 或 Azure blob 存储。  
  
-   从 Hadoop 或 Azure blob 存储查询数据，将它转换通过使用数据库的快速处理功能，并将它写回到 Hadoop 或 Azure blob 存储。  
  
 有关详细信息，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name   
    WITH (   
        LOCATION = 'hdfs_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
    AS <select_statement>  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
}  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>参数  
 [[ *database_name* 。 [ *schema_name* ]。 ] |*schema_name* 。 ] *table_name*  
 一个到三个部分组成要在数据库中创建的表的名称。 对于外部表，只是表元数据存储在关系数据库中。  
  
 LOCATION =  '*hdfs_folder*'  
 指定外部数据源的 SELECT 语句将结果写入的位置。 位置的文件夹名称，而且可以选择性地包含相对于根文件夹中的 Hadoop 群集或 Azure 存储 Blob 的路径。  如果不存在，PolyBase 将创建的路径和文件夹。  
  
 外部文件写入到*hdfs_folder*和已命名*QueryID_date_time_ID.format*，其中*ID*是增量标识符和*格式*是导出的数据格式。 例如，QID776_20160130_182739_0.orc。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含外部数据存储或将存储的位置的外部数据源对象的名称。 位置是 Hadoop 群集或 Azure 存储 Blob。 若要创建外部数据源，使用[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 指定包含外部数据文件的格式的外部文件格式对象的名称。 若要创建外部文件格式，使用[CREATE EXTERNAL FILE FORMAT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 拒绝选项  
 拒绝选项不适用于在运行此 EXTERNAL TABLE AS SELECT 语句的时间。 相反，它们是此处指定，以便数据库可以使用它们在以后当它从导入数据的外部表。 更高版本，在 CREATE TABLE AS SELECT 语句从外部表中选择数据，数据库将使用拒绝选项来确定的数值或百分比的可能无法导入之前停止导入的行。  
  
 REJECT_VALUE = *reject_value*  
 指定的值或可能无法导入之前数据库停止导入的行的百分比。  
  
 REJECT_TYPE =**值**| 百分比  
 阐明了是否 REJECT_VALUE 选项指定为文字值或百分比。  
  
 值  
 REJECT_VALUE 是文本值，而非百分比。  数据库将停止从外部数据文件导入的行时失败的行数超过*reject_value*。  
  
 例如，如果 REJECT_VALUE = 5 和 REJECT_TYPE = value，数据库将停止导入的行后 5 行无法导入。  
  
 百分比  
 REJECT_VALUE 为百分比，而非文本值。 数据库将停止从外部导入的行数据文件时*百分比*的失败的行超过了*reject_value*。 按时间间隔计算失败行百分比。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 所需当 REJECT_TYPE = 百分比，它指定要尝试导入在数据库重新计算失败行百分比之前的行的数目。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，它已尝试从外部数据文件导入 1000年行后，数据库将计算失败行百分比。 如果失败的行的百分比小于*reject_value*，数据库将尝试加载另一个 1000年行。 数据库继续进行重新计算失败行百分比之后它会尝试导入每个其他的 1000年行。  
  
> [!NOTE]  
>  由于数据库按时间间隔计算失败行百分比，失败的行的实际百分比可能会超过*reject_value*。  
  
 例如：  
  
 此示例演示三个拒绝选项如何相互交互。 例如，如果 REJECT_TYPE = 百分比，REJECT_VALUE = 30 和 REJECT_SAMPLE_VALUE = 100，可能出现以下方案：  
  
-   尝试加载的前 100 行; 数据库25 失败，而且 75 成功。  
  
-   失败行百分比将计算为 25%，这小于 30%的拒绝值。 因此，无需暂停负载。  
  
-   尝试加载的下一步 100 行; 数据库这一次 25 成功，并且 75 失败。  
  
-   50%是重新计算失败行百分比。 失败的行的百分比超过 30%拒绝值。  
  
-   负载将失败并出现失败的 50%的行在尝试加载 200 行之后的大小超过指定的 30%限制。  
  
 WITH *common_table_expression*  
 指定临时命名的结果集，这些结果集称为公用表表达式 (CTE)。 有关详细信息，请参阅[使用 common_table_expression &#40;Transact SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 选择\<select_criteria > 填充新的表的结果与 SELECT 语句。 *select_criteria*是确定要将复制到新表的数据的 SELECT 语句的正文。 SELECT 语句有关的信息，请参阅[选择 &#40;Transact SQL &#41;](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 若要运行此命令**数据库用户**需要所有的这些权限或成员身份：  
  
-   **ALTER SCHEMA**将包含新表或中的成员身份的本地架构权限**db_ddladmin**固定的数据库角色。  
  
-   **CREATE TABLE**权限或中的成员身份**db_ddladmin**固定的数据库角色。  
  
-   **选择**中引用的任何对象权限*select_criteria*。  
  
 该登录名需要所有这些权限：  
  
-   **ADMINISTER BULK OPERATIONS**权限  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**权限  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**权限  
  
-   登录名必须具有写权限以便读取和写入的 Hadoop 群集或 Azure 存储 Blob 上的外部文件夹。  
 
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 权限授予任何主体能够创建和修改任何外部数据源对象，并因此，它还授予访问数据库上的所有数据库范围凭据的功能。 此权限必须被视为高特权级别，并因此必须被授予到受信任的主体仅在系统中。
  
## <a name="error-handling"></a>错误处理  
 当 EXTERNAL TABLE AS SELECT 将数据导出到文本分隔的文件时，没有拒绝文件无法导出的行。  
  
 当创建外部表，数据库将尝试连接到外部的 Hadoop 群集或 Azure 存储 Blob。 如果连接失败，该命令将失败，并将不会创建外部表。 可能需要一分钟或更高，面向命令失败自数据库重试连接至少 3 次。  
  
 如果 CREATE EXTERNAL TABLE AS SELECT 被取消或失败，数据库将使一次性尝试删除任何新的文件和已创建外部数据源上的文件夹。  
  
 数据库将报告数据导出过程的外部数据源发生的任何 Java 错误。  
  
##  <a name="GeneralRemarks"></a>一般备注  
 CETAS 语句完成后，你可以运行[!INCLUDE[tsql](../../includes/tsql-md.md)]外部表的查询。 这些操作将数据导入数据库的查询的持续时间内除非通过使用 CREATE TABLE AS SELECT 语句导入。  
  
 外部表名称和定义存储在数据库元数据。 数据存储在外部数据源。  
  
 外部文件被命名为 *QueryID_date_time_ID.format*，其中 *ID* 是增量标识符， *format* 是导出的数据格式。 例如，QID776_20160130_182739_0.orc。  
  
 CETAS 语句始终创建未分区表，即使源表进行分区。  
  
 对于查询计划，使用创建解释，databaseuses 外部表的这些查询计划操作：  
  
-   外部随机排布移动  
  
-   外部广播移动  
  
-   外部分区移动  
  
 **适用于：**[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]作为创建外部表的必备组件，设备管理员需要配置 hadoop 连接。 有关详细信息，请参阅配置连接到外部数据 (Analytics Platform System) AP 文档可以从下载该[此处](http://www.microsoft.com/download/details.aspx?id=48241)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 由于外部表数据位于外部的数据库，备份和还原操作将仅在数据存储在数据库上运行。 这意味着只有元数据将备份和还原。  
  
 数据库还原的数据库备份中包含外部表时，不验证到外部数据源的连接。 如果原始的源不可访问，外部表的元数据还原也仍会成功，但对外部表的 SELECT 操作将失败。  
  
 数据库不能保证并且外部数据之间的数据一致性。 你的客户，是负完全责任，外部数据和数据库之间保持一致。  
  
 外部表上不支持数据操作语言 (DML) 操作。 例如，不能使用[!INCLUDE[tsql](../../includes/tsql-md.md)]更新、 插入或删除[!INCLUDE[tsql](../../includes/tsql-md.md)]语句来修改外部数据。  
  
 创建表、 DROP TABLE、 创建统计信息、 DROP STATISTICS、 创建视图和 DROP VIEW 是允许对外部表的唯一数据定义语言 (DDL) 操作。  
  
 PolyBase 可以使用每个文件夹的 33 k 文件最的多 32 个并发的 PolyBase 查询运行时。 此最大的数字包括每个 HDFS 文件夹中文件和子文件夹。 如果并发程度，小于 32 的用户可以对包含多个 33 k 文件的 HDFS 中的文件夹运行 PolyBase 查询。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]Hadoop 和 PolyBase 的建议用户保持短的文件路径，并每个 HDFS 文件夹使用不超过 30 万个文件。 在引用的文件太多时 JVM 内存不足异常时发生。  
  
 [设置行计数 &#40;Transact SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)此 CREATE EXTERNAL TABLE AS SELECT 没有影响。 若要实现类似的行为，使用[顶部 &#40;Transact SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
 当 EXTERNAL TABLE AS SELECT 选择从 RCFile 时，RCFile 中的列值不能包含管道 | 字符。  
  
## <a name="locking"></a>锁定  
 采用 SCHEMARESOLUTION 对象上的共享的锁。  
  
##  <a name="Examples"></a> 示例  
  
### <a name="a-create-a-hadoop-table-using-create-external-table-as-select-cetas"></a>A. 创建 Hadoop 表使用创建外部表 AS 选择 (CETAS)  
 下面的示例创建名为的新外部表`hdfsCustomer`，使用列定义和数据从源表`dimCustomer`。  
  
 表定义存储在数据库中，而 SELECT 语句的结果导出到 / pdwdata/customer.tbl Hadoop 外部数据源的文件*customer_ds*。 该文件的格式根据外部文件格式*customer_ff*。  
  
 文件名称生成的数据库，并包含易于对齐的文件与生成它的查询的查询 ID。  
  
 路径`hdfs://xxx.xxx.xxx.xxx:5000/files/`前面自定义目录必须已存在。 但是，如果自定义目录不存在，则数据库将创建目录。  
  
> [!NOTE]  
>  此示例指定为 5000。 如果未指定端口，则数据库使用 8020 用作默认端口。  
  
 位置和文件名称将生成 Hadoop `hdfs:// xxx.xxx.xxx.xxx:5000/files/Customer/ QueryID_YearMonthDay_HourMinutesSeconds_FileIndex.txt.`。  
  
```  
  
      -- Example is based on AdventureWorks   
CREATE EXTERNAL TABLE hdfsCustomer  
WITH (  
        LOCATION='/pdwdata/customer.tbl',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
) AS SELECT * FROM dimCustomer;  
```  
  
### <a name="b-use-a-query-hint-with-create-external-table-as-select-cetas"></a>B. 使用查询提示与创建外部表 AS 选择 (CETAS)  
 此查询显示使用 CETAS 语句的查询联接提示的基本语法。 提交该查询后数据库将使用哈希联接策略来生成查询计划。 有关联接提示以及如何使用 OPTION 子句的详细信息，请参阅[OPTION 子句 &#40;Transact SQL &#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
> [!NOTE]  
>  此示例指定为 5000。 如果未指定端口，则数据库使用 8020 用作默认端口。  
  
```  
  
      -- Example is based on AdventureWorks  
CREATE EXTERNAL TABLE dbo.FactInternetSalesNew  
WITH   
    (   
        LOCATION = '/files/Customer',  
        DATA_SOURCE = customer_ds,  
        FILE_FORMAT = customer_ff  
    )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
 [创建 TABLE &#40;Azure SQL 数据仓库、 并行数据仓库和 #41;](~/t-sql/statements/create-table-azure-sql-data-warehouse.md)   
 [创建 TABLE AS SELECT &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  


