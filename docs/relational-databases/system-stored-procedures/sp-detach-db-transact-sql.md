---
title: sp_detach_db (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
caps.latest.revision: 86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0f17581782cea310bcfad9ec6d7ce4823d1d38c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260763"
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从服务器实例中分离当前未使用的数据库，并且可以选择在分离之前为所有表运行 UPDATE STATISTICS。  
  
> [!IMPORTANT]  
>  要分离复制的数据库，该数据库必须是未发布的数据库。 有关详细信息，请参阅本主题中后面的"备注"部分。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@dbname =** ] **'***database_name***'**  
 要分离的数据库的名称。 *database_name*是**sysname**具有默认值为 NULL 值。  
  
 [ **@skipchecks =** ] **'***skipchecks***'**  
 指定跳过还是运行 UPDATE STATISTIC。 *同时将 skipchecks*是**nvarchar(10)** 具有默认值为 NULL 值。 若要跳过更新统计信息，请指定**true**。 若要显式运行更新统计信息，请指定**false**。  
  
 默认情况下，执行 UPDATE STATISTICS 可更新有关表和索引中的数据的信息。 对于要移动到只读介质的数据库，执行 UPDATE STATISTICS 非常有用。  
  
 [ **@keepfulltextindexfile=** ] **'***KeepFulltextIndexFile***'**  
 指定在数据库分离操作过程中不会删除与所分离的数据库关联的全文索引文件。 *KeepFulltextIndexFile*是**nvarchar(10)** 默认值为值**true**。 如果*KeepFulltextIndexFile*是**false**、 与数据库关联的全文索引的所有文件和全文索引的元数据会被丢弃，除非该数据库是只读的。 如果为 NULL 或**true**，全文索引相关元数据将保留。  
  
> [!IMPORTANT]  
>  **@keepfulltextindexfile**的未来版本中将删除参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 请不要在新的开发工作中使用此参数，并尽快修改当前仍在使用此参数的应用程序。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 分离数据库时，会删除其所有元数据。 如果该数据库是默认数据库的任何登录帐户， **master**将成为其默认数据库。  
  
> [!NOTE]  
>  有关如何查看登录名的所有帐户的默认数据库的信息，请参阅[sp_helplogins &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)。 如果你具有所需的权限，则可以使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)为登录名分配新的默认数据库。  
  
## <a name="restrictions"></a>限制  
 如果符合下列任一条件，则无法分离数据库：  
  
-   该数据库当前正在使用。 有关详细信息，请参阅本主题后面的“获取独占访问权限”。  
  
-   如果已进行复制，则数据库已发布。  
  
     可以分离数据库之前，您必须通过运行禁用发布[sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。  
  
    > [!NOTE]  
    >  如果无法使用 **sp_replicationdboption**，可以通过运行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)删除复制。  
  
-   数据库中存在数据库快照。  
  
     必须首先删除所有数据库快照，然后才能分离数据库。 有关详细信息，请参阅 [删除数据库快照 (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)实例。  
  
    > [!NOTE]  
    >  不能分离或附加数据库快照。  
  
-   该数据库正在进行镜像。  
  
     在终止数据库镜像会话之间，无法分离该数据库。 有关详细信息，请参阅 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)。  
  
-   数据库处于可疑状态。  
  
     您必须先将可疑数据库设为紧急模式，然后才能对其进行分离。 有关如何将数据库置于紧急模式下的详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
  
-   数据库为系统数据库。  
  
## <a name="obtaining-exclusive-access"></a>获取独占访问权限  
 分离数据库需要对数据库有独占访问权限。 如果要分离的数据库正在使用当中，则必须先将该数据库设置为 SINGLE_USER 模式以获取独占访问权限，然后才能对其进行分离。  
  
 例如，以下`ALTER DATABASE`语句获取独占访问权限[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库后从数据库断开所有当前用户的连接。  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  若要强制当前出数据库的用户立即或在指定的秒数，还使用回滚选项： ALTER DATABASE *database_name* WITH ROLLBACK 设置 SINGLE_USER *rollback_option*. 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="reattaching-a-database"></a>重新附加数据库  
 可以使用 CREATE DATABASE（带有 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 选项）保留并重新附加分离文件。 这些文件可以移动并附加到其他服务器上。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或中的成员身份**db_owner**数据库的角色。  
  
## <a name="examples"></a>示例  
 以下示例将分离[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库与*同时将 skipchecks*设置为 true。  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 以下示例将分离 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库，并保留全文索引文件和全文索引的元数据。 此命令将运行 UPDATE STATISTICS，这是默认行为。  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [分离数据库](../../relational-databases/databases/detach-a-database.md)  
  
  
