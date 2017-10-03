---
title: "CREATE DATABASE （Azure SQL 数据库） |Microsoft 文档"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: e9781bd657f094c7be57ae513cc2c4a026ad4746
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  创建新数据库。  
  
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
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

[ AS COPY OF [source_server_name.]source_database_name ]

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>参数  
 此语法关系图说明了 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中支持的参数。  
  
 *database_name*  
 新数据库的名称。 此名称必须是唯一的 SQL server，其中可托管同时[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]数据库和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]数据库，并应符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
 *Collation_name*  
 指定数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果未指定，则会为数据库分配默认排序规则（也即 SQL_Latin1_General_CP1_CI_AS）。  
  
 Windows 和 SQL 排序规则名称，有关详细信息[COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
 *CATALOG_COLLATION*  
指定的元数据目录的默认排序规则。 *DATABASE_DEFAULT*指定元数据目录用于系统视图和系统表进行整理，以匹配数据库的默认排序规则。  这是在 SQL Server 中找到的行为。 

*SQL_Latin1_General_CP1_CI_AS*指定元数据目录用于系统视图和表进行整理到固定 SQL_Latin1_General_CP1_CI_AS 排序规则。  如果未指定，这是 Azure SQL 数据库上的默认设置。

 *版本*  
 指定数据库的服务层。 可用值有: 基本、 标准、 高级和 premiumrs。  
  
 如果指定版本，但未指定 MAXSIZE，MAXSIZE 设置为该版本支持的限制性最强大小。  
  
 *最大大小*  
 指定数据库的最大大小。 MAXSIZE 必须对指定 EDITION（服务层）有效。下面是服务层支持的 MAXSIZE 值和默认值 (D)。  
  
|**最大大小**|**基本**|**S0 S2**|**S3 S12**|**P1 P6 和 PRS1 PRS6**| **P11 P15** 
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
|从 1024 GB 达 4096 GB 的增量的 256 GB * |N/A|N/A|N/A|N/A|√|√|  
  
 \*P11 和 P15 允许 MAXSIZE 达 4 TB 1024 gb 正在默认大小。  P11 和 P15 可以使用 4 TB 的包含存储，并且不额外收费。 在高级层中，最大大小大于 1 TB 是当前在以下区域中提供： 美国 East2、 美国西部、 US Gov Virginia、 西欧、 德国中央、 南部亚洲东部、 日本东部、 澳大利亚东部、 加拿大中央和加拿大东部。 当前限制，请参阅[单一数据库](https://docs.microsoft.com/azure/sql-database-single-database-resources)。  
  
 以下规则适用于 MAXSIZE 和 EDITION 参数：  
  
-   MAXSIZE 值（如果指定）必须是上表中显示的有效值。  
  
-   如果指定了 EDITION 但未指定 MAXSIZE，使用版本的默认值。 例如，如果版本设置为标准，并且未指定最大大小，则最大大小自动设置为 250 MB。  
  
-   如果 MAXSIZE 和 EDITION 均未指定，则版本设置为标准 (S0)，并最大大小设置为 250 GB。  
  
 SERVICE_OBJECTIVE  
 指定性能级别。 服务目标说明和有关大小、 版本，以及服务目标组合的详细信息，请参阅[Azure SQL 数据库服务层和性能级别](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[SQL 数据库资源限制](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits)。 如果 EDITION 不支持指定的 SERVICE_OBJECTIVE，你会收到一个错误。  
  
 ELASTIC_POOL (名称 = \<elastic_pool_name >) 若要在弹性数据库池中创建新的数据库，设置数据库的 SERVICE_OBJECTIVE 为 ELASTIC_POOL 并提供的池的名称。 有关详细信息，请参阅[创建和管理 SQL 数据库弹性数据库池 （预览版）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。  
  
 *作为 COPY OF [source_server_name。]source_database_name*  
 将数据库复制到同一台或其他 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器上。  
  
 *source_server_name*  
 源数据库所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的名称。 当源数据库和目标数据库位于同一台 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器上时，此参数是可选的。  
  
 注意：`AS COPY OF` 参数不支持完全限定的唯一域名。 换言之，如果您的服务器的完全限定域名是 `serverName.database.windows.net`，则在数据库复制期间仅使用 `serverName`。  
  
 *source_database_name*  
 要复制的数据库的名称。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]不支持以下参数和选项，使用时`CREATE DATABASE`语句：  
  
-   参数会相关到的物理位置的文件，如\<filespec > 和\<文件组 >  
  
-   外部访问选项，如 DB_CHAINING 和 TRUSTWORTHY  
  
-   附加数据库  
  
-   Service Broker 选项，如 ENABLE_BROKER、NEW_BROKER 和 ERROR_BROKER_CONVERSATIONS  
  
-   数据库快照  
  
 有关参数的详细信息和`CREATE DATABASE`语句，请参阅[CREATE DATABASE & #40;SQL Server Transact SQL & #41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>注释  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的数据库具有多个在创建数据库时设置的默认设置。 有关这些默认设置的详细信息，请参阅中的值列表[DATABASEPROPERTYEX & #40;Transact SQL & #41;](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE 提供限制数据库大小的功能。 如果数据库的大小达到其 MAXSIZE，您将收到错误代码 40544。 如果发生这种情况，您不能插入或更新数据或创建新的对象（如表、存储过程、视图和函数）。 不过，您仍可以读取和删除数据、截断表、删除表和索引以及重新建立索引。 然后，您可以将 MAXSIZE 更新为比当前数据库大小更大的值，或者删除一些数据以释放存储空间。 在您可以插入新数据之前，可能有长达十五分钟的延迟。  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 语句必须是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的唯一语句。 
  
 若要以后更改大小、 版本或服务目标值，使用[ALTER DATABASE & #40;Azure SQL Database & #41;](../../t-sql/statements/alter-database-azure-sql-database.md).  

创建数据库期间 CATALOG_COLLATION 参数才可用。 
  
## <a name="database-copies"></a>数据库副本  
 复制数据库使用`CREATE DATABASE`语句是一个异步操作。 因此，在整个复制过程中，不需要与 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器建立连接。 `CREATE DATABASE`语句将控制权返回给用户 sys.databases 中的项在创建之后且在数据库副本之前的操作已完成。 换言之，当数据库复制仍在进行时，`CREATE DATABASE` 语句会成功返回。  
  
-   监视复制过程[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]服务器： 查询`percentage_complete`或`replication_state_desc`中的列[dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)或`state`中的列**sys.databases**视图。 [Sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)可以使用视图以及它将返回包括数据库副本的数据库操作的状态。  
  
 在复制过程成功完成后，目标数据库与源数据库在事务上是一致的。  
  
 以下语法和语义规则应用于您对 `AS COPY OF` 参数的使用：  
  
-   源服务器名称与复制目标的服务器名称可能相同，也可能不同。 它们相同时，此参数是可选的默认情况下使用当前会话的服务器上下文。  
  
-   必须指定源数据库名称和目标数据库名称，并且这些名称必须唯一且符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标识符规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
-   必须在将创建新数据库的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的 master 数据库的上下文中执行 `CREATE DATABASE` 语句。  
  
-   在复制完成之后，必须将目标数据库作为独立的数据库进行管理。 您可以独立于源数据库，针对新数据库执行 `ALTER DATABASE` 和 `DROP DATABASE` 语句。 您还可以将新数据库复制到另一个新数据库。  
  
-   当正在进行数据库复制时，可以继续访问源数据库。  
  
 有关详细信息，请参阅[创建一份 Azure SQL 数据库使用 TRANSACT-SQL](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)。  
  
## <a name="permissions"></a>Permissions  
 若要创建数据库登录名必须是以下项之一：  
  
-   服务器级别主体登录名  
  
-   本地 Azure SQL 服务器的 Azure AD 管理员  
  
-   是的成员的登录名`dbmanager`数据库角色  
  
 **使用的其他要求`CREATE DATABASE ... AS COPY OF`语法：**本地服务器上执行该语句的登录名还必须是至少`db_owner`源服务器上。 如果登录名基于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，在本地服务器上执行的语句的登录名必须匹配的登录名对源[!INCLUDE[ssSDS](../../includes/sssds-md.md)]服务器，具有相同名称和密码。  
  
## <a name="examples"></a>示例  
向你演示如何连接到 Azure SQL 数据库使用 SQL Server Management Studio 的快速入门教程，请参阅[Azure SQL 数据库： 使用 SQL Server Management Studio 来连接和查询数据](/azure/sql-database/sql-database-connect-query-ssms)。  
  
### <a name="simple-example"></a>简单示例  
 一个简单的示例，用于创建数据库。  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>使用版的简单示例  
 一个简单的示例，用于创建标准数据库。  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>使用其他选项的示例  
 使用多个选项的示例。  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>创建副本  
 示例创建数据库的副本。  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>在弹性池中创建数据库  
 名为 S3M100 池内创建新的数据库：  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>在另一台服务器上创建数据库的副本  
 下面的示例创建名 db_copy P2 性能级别为单个数据库的 db_original 数据库的副本。  这是 true，无论 db_original 是否在弹性池或单个数据库的性能级别。  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 下面的示例创建名为 db_copy 名为 ep1 弹性池中的 db_original 数据库的副本。  这是 true，无论 db_original 是否在弹性池或单个数据库的性能级别。  如果 db_original 处于弹性池的一个不同的名称，然后在 ep1 仍创建 db_copy。  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>使用指定的目录排序规则值创建数据库

下面的示例设置要与数据库排序规则相同的目录排序规则的数据库创建期间将目录排序规则设置为 DATABASE_DEFAULT。

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>另请参阅  

-  [sys.dm_database_copies & #40;Azure SQL Database & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE & #40;Azure SQL Database & #41;](alter-database-azure-sql-database.md)   
    
  


