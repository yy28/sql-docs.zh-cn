---
title: CREATE DATABASE（Azure SQL 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 54b565a15310eaa9d0e8d2dbac39e28ca55ea1e5
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  创建新数据库。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

## <a name="syntax"></a>语法  

``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n]) 
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | ( EDITION = {  'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' } 
  | SERVICE_OBJECTIVE = 
    {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
      | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE = 
      {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
        | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
        | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
        | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
        | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
  ]  
 [;] 
 
```  
  
## <a name="arguments"></a>参数  
 此语法关系图说明了 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中支持的参数。  
  
*database_name* 
 
新数据库的名称。 此名称在 SQL Server 上必须是唯一的，它可托管 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 数据库和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 数据库，且符合标识符的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
*Collation_name*  

指定数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果未指定，则会为数据库分配默认排序规则（也即 SQL_Latin1_General_CP1_CI_AS）。  
  
有关 Windows 和 SQL 排序规则名称的详细信息，请参阅 [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
CATALOG_COLLATION  

指定元数据目录的默认排序规则。 *DATABASE_DEFAULT* 指定用于系统视图和系统表的元数据目录按数据库的默认排序规则进行整理。  这是在 SQL Server 中所发现的行为。 

*SQL_Latin1_General_CP1_CI_AS* 指定用于系统视图和表的元数据目录按固定的 SQL_Latin1_General_CP1_CI_AS 排序规则进行整理。  如果未指定，这将是 Azure SQL 数据库上的默认设置。

EDITION
 
指定数据库的服务层。 可用的值包括：“basic”、“standard”、“premium”、“GeneralPurpose”和“BusinessCritical”。 已删除对“premiumrs”的支持。 如有问题，请使用此电子邮件别名：premium-rs@microsoft.com。
  
 在指定了 EDITION 但未指定 MAXSIZE 时，MAXSIZE 将设置为版本支持的限制性最高的大小。  
  
 MAXSIZE

指定数据库的最大大小。 MAXSIZE 必须对指定 EDITION（服务层）有效。下面是服务层支持的 MAXSIZE 值和默认值 (D)。

**基于 DTU 的模型**

|**MAXSIZE**|**基本**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** | 
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------| 
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|
|500 MB|√|√|√|√|√|
|1 GB|√|√|√|√|√|
|2 GB|√ (D)|√|√|√|√|
|5 GB|N/A|√|√|√|√|
|10 GB|N/A|√|√|√|√|
|20 GB|N/A|√|√|√|√|
|30 GB|N/A|√|√|√|√|
|40 GB|N/A|√|√|√|√|
|50 GB|N/A|√|√|√|√|
|100 GB|N/A|√|√|√|√|
|150 GB|N/A|√|√|√|√|
|200 GB|N/A|√|√|√|√|
|250 GB|N/A|√ (D)|√ (D)|√|√|
|300 GB|N/A|N/A|√|√|√|
|400 GB|N/A|N/A|√|√|√|
|500 GB|N/A|N/A|√|√ (D)|√|
|750 GB|N/A|N/A|√|√|√|
|1024 GB|N/A|N/A|√|√|√ (D)|
|从 1024 GB 到最大 4096 GB，增量为 256 GB* |N/A|N/A|N/A|N/A|√|√|  
  
\* P11 和 P15 允许 MAXSIZE 达到 4 TB，默认大小为 1024 GB。  P11 和 P15 可以使用最大 4 TB 的内含存储，且无需额外费用。 在高级层中，以下区域当前提供大于 1 TB 的 MAXSIZE：美国东部 2、美国西部、美国弗吉尼亚州政府、西欧、德国中部、东南亚、日本东部、澳大利亚东部、加拿大中部和加拿大东部。 有关基于 DTU 的模型的资源限制的其他详细信息，请参阅[基于 DTU 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。  

基于 DTU 的模型的 MAXSIZE 值（如果指定）必须为上表中所示的指定服务层的有效值。
 
**基于 vCore 的模型**

**常规用途服务层**
|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|最大数据大小 (GB)|1024|1024|1536|3072|4096|

**业务关键型服务层**
|性能级别|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|最大数据大小 (GB)|1024|1024|1536|2048|2048|

如果使用 vCore 模型时未设置 `MAXSIZE` 值，则默认为 32 GB。 有关基于 vCore 的模型的资源限制的其他详细信息，请参阅[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。
  
以下规则适用于 MAXSIZE 和 EDITION 参数：  
  
- 如果指定了 EDITION 但未指定 MAXSIZE，则使用版本的默认值。 例如，如果 EDITION 设置为 Standard 并且未指定 MAXSIZE，则 MAXSIZE 将自动设置为 250 MB。  
- 如果 MAXSIZE 和 EDITION 均未指定，则 EDITION 设置为 Standard (S0)，MAXSIZE 设置为 250 GB。  

SERVICE_OBJECTIVE

指定性能级别。 服务目标的可用值包括：`S0`、`S1`、`S2`、`S3`、`S4`、`S6`、`S7`、`S9`、`S12`、`P1`、`P2`、`P4`、`P6`、`P11`、`P15`、`GP_GEN4_1`、`GP_GEN4_2`、`GP_GEN4_4`、`GP_GEN4_8`、`GP_GEN4_16`、`BC_GEN4_1`、`BC_GEN4_2`、`BC_GEN4_4`、`BC_GEN4_8`、`BC_GEN4_16`。 

有关服务目标说明以及大小、版本和服务目标组合的详细信息，请参阅 [Azure SQL 数据库服务层](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)。 如果 EDITION 不支持指定的 SERVICE_OBJECTIVE，你会收到一个错误。 若要将 SERVICE_OBJECTIVE 值从一层更改为另一层（例如从 S1 更改为 P1），还必须更改 EDITION 值。 有关服务目标说明以及大小、版本和服务目标组合的详细信息，请参阅 [Azure SQL 数据库服务层和性能级别](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)、[基于 DTU 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)和[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。  删除了对 PRS 服务目标的支持。 如有问题，请使用此电子邮件别名：premium-rs@microsoft.com。 
  
ELASTIC_POOL (name = \<elastic_pool_name)
 
要在弹性数据库池中创建新数据库，请将数据库的 SERVICE_OBJECTIVE 设置为 ELASTIC_POOL，并提供池的名称。 有关详细信息，请参阅[创建和管理 SQL 数据库弹性数据库池 （预览版）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。  
  
AS COPY OF [source_server_name.]source_database_name

将数据库复制到同一台或其他 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器上。  
  
*source_server_name*  

源数据库所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的名称。 当源数据库和目标数据库位于同一台 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器上时，此参数是可选的。  
  
> [!NOTE]
> `AS COPY OF` 参数不支持完全限定的唯一域名。 换言之，如果您的服务器的完全限定域名是 `serverName.database.windows.net`，则在数据库复制期间仅使用 `serverName`。  
  
*source_database_name*

要复制的数据库的名称。  
  
使用 `CREATE DATABASE` 语句时，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 不支持以下参数和选项：  
  
- 与文件的物理放置相关的参数，例如 \<filespec> 和 \<filegroup>  
  
- 外部访问选项，如 DB_CHAINING 和 TRUSTWORTHY  
  
- 附加数据库  
  
- Service Broker 选项，如 ENABLE_BROKER、NEW_BROKER 和 ERROR_BROKER_CONVERSATIONS  
  
- 数据库快照  
  
有关参数和 `CREATE DATABASE` 语句的详细信息，请参阅 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks
 
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的数据库具有多个在创建数据库时设置的默认设置。 有关这些默认设置的详细信息，请参阅 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) 中的值列表。  
  
MAXSIZE 提供限制数据库大小的功能。 如果数据库的大小达到其 MAXSIZE，你将收到错误代码 40544。 如果发生这种情况，您不能插入或更新数据或创建新的对象（如表、存储过程、视图和函数）。 不过，您仍可以读取和删除数据、截断表、删除表和索引以及重新建立索引。 然后，您可以将 MAXSIZE 更新为比当前数据库大小更大的值，或者删除一些数据以释放存储空间。 在您可以插入新数据之前，可能有长达十五分钟的延迟。  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 语句必须是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的唯一语句。 
  
若要在以后更改大小、版本或服务目标值，请使用 [ALTER DATABASE（Azure SQL 数据库）](../../t-sql/statements/alter-database-azure-sql-database.md)。  

CATALOG_COLLATION 参数仅在数据库创建期间可用。 
  
## <a name="database-copies"></a>数据库复制  

使用 `CREATE DATABASE` 语句复制数据库是一个异步操作。 因此，在整个复制过程中，不需要与 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器建立连接。 `CREATE DATABASE` 语句会在 sys.databases 中的条目创建之后，但是在数据库复制操作完成之前将控制权返还给用户。 换言之，当数据库复制仍在进行时，`CREATE DATABASE` 语句会成功返回。  
  
- 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 服务器上监视复制进程：在 [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) 中查询 `percentage_complete` 或 `replication_state_desc` 列，或在 **sys.databases** 视图中查询 `state` 列。 可以使用 [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 视图，它还会返回数据库操作（包括数据库复制）的状态。  
  
在复制过程成功完成后，目标数据库与源数据库在事务上是一致的。  
  
以下语法和语义规则应用于您对 `AS COPY OF` 参数的使用：  
  
- 源服务器名称与复制目标的服务器名称可能相同，也可能不同。 如果相同，此参数是可选的，默认情况下将使用当前会话的服务器上下文。  
  
- 必须指定源数据库名称和目标数据库名称，并且这些名称必须唯一且符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标识符规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
- 必须在将创建新数据库的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的 master 数据库的上下文中执行 `CREATE DATABASE` 语句。 
- 在复制完成之后，必须将目标数据库作为独立的数据库进行管理。 您可以独立于源数据库，针对新数据库执行 `ALTER DATABASE` 和 `DROP DATABASE` 语句。 您还可以将新数据库复制到另一个新数据库。  
  
- 当正在进行数据库复制时，可以继续访问源数据库。  
  
 有关详细信息，请参阅[使用 TRANSACT-SQL 创建 Azure SQL 数据库的副本](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)。  
  
## <a name="permissions"></a>权限  
 要创建数据库，登录名必须为下列各项之一：  
  
- 服务器级别主体登录名  
  
- 本地 Azure SQL Server 的 Azure AD 管理员  
  
- 登录名为 `dbmanager` 数据库角色的成员  
  
 **使用 `CREATE DATABASE ... AS COPY OF` 语法的其他要求：**在本地服务器上执行语句的登录名还必须至少为源服务器上的 `db_owner`。 如果登录名基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，那么在本地服务器上执行语句的登录名必须在源 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器上具有匹配的登录名，名称和密码均完全相同。  
  
## <a name="examples"></a>示例  
有关如何使用 SQL Server Management Studio 连接到 Azure SQL 数据库 的快速入门教程，请参阅 [Azure SQL 数据库：使用 SQL Server Management Studio 连接和查询数据](/azure/sql-database/sql-database-connect-query-ssms)。  
  
### <a name="simple-example"></a>简单示例  
 创建数据库的简单示例。  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>版本的简单示例  
 创建标准数据库的简单示例。  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>其他选项的示例  
 使用多个选项的示例。  
  
```sql  
CREATE DATABASE hito 
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS 
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>创建副本  
 创建数据库副本的示例。  
  
```sql  
CREATE DATABASE escuela 
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>在弹性池中创建数据库  
 在名为 S3M100 的池中创建新数据库：  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>在其他服务器上创建数据库副本  
 下面的示例针对单个数据库，在 P2 性能级别下创建名为 db_copy 的 db_original 数据库的副本。  无论 db_original 是否位于弹性池中或是否处于单个数据库的性能级别，这都为 true。  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 下面的示例在名为 ep1 的弹性池中创建名为 db_copy 的 db_original 数据库的副本。  无论 db_original 是否位于弹性池中或是否处于单个数据库的性能级别，这都为 true。  如果 db_original 位于具有不同名称的弹性池中，那么仍将在 ep1 中创建 db_copy。  
  
```sql  
CREATE DATABASE db_copy 
  AS COPY OF ozabzw7545.db_original 
  (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>使用指定的目录排序规则值创建数据库

下面的示例在数据库创建期间将目录排序规则设置为 DATABASE_DEFAULT，其会将目录排序规则设置为与数据库排序规则相同。

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
  WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>另请参阅  

-  [sys.dm_database_copies（Azure SQL 数据库）](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

- [ALTER DATABASE（Azure SQL 数据库）](alter-database-azure-sql-database.md) 
  
  

