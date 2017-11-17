---
title: "DATABASEPROPERTYEX (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
caps.latest.revision: 84
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 737aed43128be71a53c8087be11176bc4e364e8a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中指定数据库的指定数据库选项或属性的当前设置。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>参数  
*database*  
是一个表达式来表示为其返回命名的属性信息数据库的名称。 *数据库*是**nvarchar （128)**。  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 必须是当前数据库的名称。 如果提供不同的数据库名称，所有属性返回为 NULL。
  
*属性*  
表示要返回的数据库属性的名称的表达式。 *属性*是**varchar （128)**，和可以是以下值之一。 返回类型是**sql_variant**。 下表显示了各属性值的基本数据类型。
  
> [!NOTE]  
>  如果数据库未启动，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过直接访问数据库而不是通过从元数据检索值而检索到的属性将返回 NULL。 即，数据库的 AUTO_CLOSE 设置为 ON，或者数据库已脱机。  
  
|属性|Description|返回的值|  
|---|---|---|
|排序规则|数据库的默认排序规则名称。|排序规则名称<br /><br /> NULL = 数据库没有启动。<br /><br /> 基数据类型： **nvarchar （128)**|  
|ComparisonStyle|排序规则的 Windows 比较样式。 ComparisonStyle 是通过使用以下值可能样式计算的位图。<br /><br /> 忽略大小写： 1<br /><br /> 忽略重音： 2<br /><br /> 忽略假名： 65536<br /><br /> 忽略宽度： 131072<br /><br /> <br /><br /> 例如，196609 的默认值是将忽略大小写、忽略假名和忽略宽度选项合并在一起的结果。|返回比较样式。<br /><br /> 对所有二进制排序规则均返回 0。<br /><br /> 基数据类型： **int**|  
|版本|数据库版本或服务层。|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]， [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。<br /><br /> <br /><br /> Web = Web Edition 数据库<br /><br /> Business = Business Edition 数据库<br /><br /> 基本<br /><br /> Standard<br /><br /> Premium<br /><br /> 系统 （为 master 数据库） 的<br /><br /> NULL = 数据库没有启动。<br /><br /> 基数据类型： **nvarchar**(64)|  
|IsAnsiNullDefault|数据库遵循 ISO 规则，允许 Null 值。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAnsiNullsEnabled|所有与 Null 的比较将取值为未知。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAnsiPaddingEnabled|在比较或插入前，字符串将被填充到相同长度。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAnsiWarningsEnabled|如果发生了标准错误条件，则将发出错误消息或警告消息。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsArithmeticAbortEnabled|如果执行查询时发生溢出或被零除错误，则将结束查询。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAutoClose|在最后一个用户退出后，数据库完全关闭并释放资源。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAutoCreateStatistics|查询优化器根据需要创建单列统计信息以提高查询性能。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAutoCreateStatisticsIncremental|如果可能，自动创建的单列统会信息会递增。|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAutoShrink|可以定期自动收缩数据库文件。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsAutoUpdateStatistics|当查询使用现有统计信息并且该统计信息可能过期时，查询优化器将更新该统计信息。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|
|IsClone|数据库是架构和统计信息的唯一副本，用户数据库。|**适用于**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**| 
|IsCloseCursorsOnCommitEnabled|提交事务时关闭打开的游标。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsFulltextEnabled|支持对数据库进行全文和语义索引。|**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**<br /><br /> **注意：**此属性的值不起作用。 用户数据库始终启用全文搜索。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中将删除此列。 请不要在新的开发工作中使用此列，并尽快修改当前还在使用任何这些列的应用程序。|  
|IsInStandBy|数据库以只读方式联机，并允许还原日志。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsLocalCursorsDefault|游标声明默认为 LOCAL。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|在会话设置 TRANSACTION ISOLATION LEVEL 设置为较低的隔离级别、READ COMMITTED 或 READ UNCOMMITTED 时，使用 SNAPSHOT 隔离访问内存优化表。|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> 基数据类型： **int**|  
|IsMergePublished|如果安装了复制，则可以发布数据库表供合并复制。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsNullConcat|Null 串联操作数产生 NULL。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsNumericRoundAbortEnabled|表达式中缺少精度时将产生错误。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsParameterizationForced|PARAMETERIZATION 数据库 SET 选项为 FORCED。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效|  
|IsQuotedIdentifiersEnabled|可对标识符使用英文双引号。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsPublished|如果安装了复制，可以发布数据库表供快照复制或事务复制。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsRecursiveTriggersEnabled|已启用触发器递归触发。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsSubscribed|数据库已订阅发布。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsSyncWithBackup|数据库为发布数据库或分发数据库，并且在还原时不用中断事务复制。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsTornPageDetectionEnabled|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]检测到因电力故障或其他系统故障造成的不完全 I/O 操作。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效<br /><br /> 基数据类型： **int**|  
|IsXTPSupported|指示是否数据库支持 In-memory OLTP，即，创建和使用内存优化表和本机编译的模块。<br /><br /> 特定于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> IsXTPSupported 不依赖于存在任何 MEMORY_OPTIMIZED_DATA 文件组中，这是用于创建内存中 OLTP 对象的要求。|**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br /> **适用于**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]启动[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 输入无效，出现错误，或不适用<br /><br /> 基数据类型： **int**|  
|LCID|Windows 区域设置标识符 (LCID) 的排序规则。|LCID 值（十进制格式）。<br /><br /> 基数据类型： **int**|  
|MaxSizeInBytes|最大数据库大小（以字节为单位）。|**适用于**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]， [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL = 数据库没有启动<br /><br /> 基数据类型： **bigint**|  
|恢复|数据库的恢复模型。|FULL = 完整恢复模式<br /><br /> BULK_LOGGED = 大容量日志记录模型<br /><br /> SIMPLE = 简单恢复模式<br /><br /> 基数据类型： **nvarchar （128)**|  
|ServiceObjective|描述中的数据库的性能级别[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]或[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。|可以为以下各项之一：<br /><br /> Null： 数据库未启动<br /><br /> 已共享（针对 Web/企业版本）<br /><br /> 基本<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> 系统（针对主数据库）<br /><br /> 基数据类型： **nvarchar(32)**|  
|ServiceObjectiveId|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 中的服务器目标 ID。|**uniqueidentifier**标识服务目标。|  
|SQLSortOrder|SQL Server 早期版本中支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序顺序 ID。|0 = 数据库使用的是 Windows 排序规则<br /><br /> >0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序顺序 ID<br /><br /> NULL = 输入无效或数据库未启动<br /><br /> 基数据类型： **tinyint**|  
|状态|数据库状态。|ONLINE = 数据库可用于查询。<br /><br /> **注意：**可能会返回数据库是已打开而不是联机状态，但将其恢复。 若要确定当数据库可以接受连接时，查询的排序规则属性**DATABASEPROPERTYEX**。 在数据库排序规则返回非 Null 值之后，数据库就可以接受连接了。 对于 Always On 的数据库，查询 sys.dm_hadr_database_replica_states database_state 或 database_state_desc 列。<br /><br /> OFFLINE = 数据库已被显式置于脱机状态。<br /><br /> RESTORING = 正在还原数据库。<br /><br /> RECOVERING = 正在恢复数据库，尚不能用于查询。<br /><br /> SUSPECT = 数据库未恢复。<br /><br /> EMERGENCY = 数据库处于紧急只读状态。 只有 sysadmin 成员可进行访问。<br /><br /> 基数据类型： **nvarchar （128)**|  
|Updateability|指示是否可以修改数据。|READ_ONLY = 可读取但不能修改数据。<br /><br /> READ_WRITE = 可读取和修改数据。<br /><br /> 基数据类型： **nvarchar （128)**|  
|UserAccess|指示哪些用户可以访问数据库。|SINGLE_USER = 一次仅一个 db_owner、dbcreator 或 sysadmin 用户<br /><br /> RESTRICTED_USER = 仅限 db_owner、dbcreator 和 sysadmin 角色的成员<br /><br /> MULTI_USER = 所有用户<br /><br /> 基数据类型： **nvarchar （128)**|  
|版本|用于创建数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代码的内部版本号。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|版本号 = 数据库处于打开状态。<br /><br /> NULL = 数据库没有启动。<br /><br /> 基数据类型： **int**|  
  
## <a name="return-types"></a>返回类型
**sql_variant**
  
## <a name="exceptions"></a>异常  
出现错误时或调用方没有查看对象的权限时，将返回 NULL。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，用户只能查看其拥有的安全对象的元数据，或者已对其授予权限的安全对象的元数据。 也就是说，如果用户对该对象没有任何权限，则那些会生成元数据的内置函数（如 OBJECT_ID）可能返回 NULL。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>注释  
DATABASEPROPERTYEX 一次只返回一个属性设置。 若要显示多个属性设置，请使用[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。
  
## <a name="examples"></a>示例  
  
### <a name="a-retrieving-the-status-of-the-autoshrink-database-option"></a>A. 检索 AUTO_SHRINK 数据库选项的状态  
以下示例将返回 `AdventureWorks` 数据库的 AUTO_SHRINK 数据库选项的状态。
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]该结果集指示 AUTO_SHRINK 已关闭。
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. 检索数据库的默认排序规则  
下面的示例返回的几个特性`AdventureWorks`数据库。
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>另请参阅
[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
[数据库状态](../../relational-databases/databases/database-states.md)  
[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)
  
  

