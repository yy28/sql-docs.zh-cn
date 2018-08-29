---
title: sp_fulltext_catalog (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a95aeee70e673e0db05016eaa0cf95e2cc129439
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43087345"
---
# <a name="spfulltextcatalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  创建和删除全文目录，并启动和停止目录的索引操作。 可为每个数据库创建多个全文目录。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)， [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)，并[DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@ftcat=**] **'***fulltext_catalog_name***'**  
 全文目录名称。 每个数据库的目录名称必须是唯一的。 *fulltext_catalog_name*是**sysname**。  
  
 [  **@action=**] **'***操作*****  
 要执行的操作。 *操作*是**varchar （20)**，可以是下列值之一。  
  
> [!NOTE]  
>  可根据需要创建、删除和修改全文目录。 但请避免同时对多个目录的架构进行更改。 可以使用执行这些操作**sp_fulltext_table**存储过程，这是建议的方法。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**创建**|在文件系统中创建空的新的全文目录，并将添加中的关联的行**sysfulltextcatalogs**与*fulltext_catalog_name*并*root_directory*，（如果存在） 的值。 *fulltext_catalog_name*在数据库中必须唯一。|  
|**Drop**|放弃*fulltext_catalog_name*从文件系统中移除并删除相关的行中通过**sysfulltextcatalogs**。 如果此目录中包含一个或多个表的索引，则此操作将失败。 **sp_fulltext_table** '*table_name*'，'drop' 应执行以删除目录中的表。<br /><br /> 如果目录不存在，则会显示错误。|  
|**start_incremental**|启动增量填充*fulltext_catalog_name*。 如果目录不存在，则会显示错误。 如果一个全文索引填充已经是活动的，则会显示一个警告，而不发生填充操作。 使用增量填充仅已更改的行检索为全文索引编制索引，前提是有**时间戳**要进行全文索引表中存在的列。|  
|**start_full**|启动完全填充的*fulltext_catalog_name*。 即使与此全文目录相关联的每一个表的每一行都进行过索引，也会对其检索全文索引。|  
|**停止**|停止的索引填充*fulltext_catalog_name*。 如果目录不存在，则会显示错误。 如果已经停止了填充，则不会显示警告。|  
|**Rebuild**|重新生成*fulltext_catalog_name*。 重新生成目录时，将删除现有目录，并在其原位置创建一个新目录。 具有全文索引引用的所有表都与此新目录相关联。 重新生成会重置数据库系统表中的全文元数据。<br /><br /> 如果更改跟踪为 OFF，重新生成并不会导致重新填充新创建的全文目录。 在这种情况下，若要重新填充，请执行**sp_fulltext_catalog**与**start_full**或**start_incremental**操作。|  
  
 [ **@path=**] **'***root_directory***'**  
 为是根目录 （不是完整物理路径）**创建**操作。 *root_directory*是**nvarchar(100)** 和具有默认值为 NULL，表示使用安装时指定的默认位置。 这是 Mssql 目录中; 中的 Ftdata 子目录例如，C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\FTData。 指定的根目录必须驻留在同一台计算机的某一驱动器上，它不能只包含驱动器号，也不能是相对路径。 不支持使用网络驱动器、可移动驱动器、软盘和 UNC 路径。 全文目录必须在与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关联的本地硬盘上创建。  
  
 **@path** 仅当*操作*是**创建**。 有关以外的其他操作**创建**(**停止**，**重新生成**，等等)， **@path**必须为 NULL 或省略。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例是群集中的虚拟服务器，则指定的目录所在目录需要位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源所属的共享磁盘驱动器上。 如果@path未指定，则默认目录所在目录的位置为已安装虚拟服务器时指定的目录中的共享磁盘驱动器上。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>Remarks  
 **Start_full**操作用来创建中的全文索引数据的完整快照*fulltext_catalog_name*。 **Start_incremental**操作用来重新编制索引的数据库中仅已更改的行。 仅当表具有的类型的列，可以应用增量填充**时间戳**。 如果全文目录中的表不包含类型的列**时间戳**，则该表将进行完全填充。  
  
 全文目录及索引数据存储在某些文件中，这些文件是在全文目录所在目录中创建的。 该全文目录所在目录创建为目录中指定的目录的子目录**@path**或在该服务器默认全文目录所在目录中如果**@path**不是指定。 生成全文目录所在目录名称的方式可以保证它在服务器上是唯一的。 因此，一个服务器上所有的全文目录所在目录可以共享相同的路径。  
  
## <a name="permissions"></a>Permissions  
 调用方必须是隶属**db_owner**角色。 根据请求的操作，调用方应不拒绝授予 ALTER 或 CONTROL 权限 (这**db_owner**具有) 授予目标全文目录。  
  
## <a name="examples"></a>示例  
  
### <a name="a-create-a-full-text-catalog"></a>A. 创建全文目录  
 此示例创建一个空的全文目录**Cat_Desc**，在**AdventureWorks2012**数据库。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. 重新生成全文目录  
 此示例将重新生成现有的全文目录**Cat_Desc**，在**AdventureWorks2012**数据库。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. 启动全文目录的填充  
 此示例将开始的完全填充**Cat_Desc**目录。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. 停止全文目录的填充  
 此示例将停止的总体**Cat_Desc**目录。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. 删除全文目录  
 此示例将删除**Cat_Desc**目录。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [FULLTEXTCATALOGPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)  
  
  
