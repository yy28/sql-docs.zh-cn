---
title: sp_replicationdboption (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4f7329894132d051e2cd526fd339a4511e2ac196
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置指定数据库的复制数据库选项。 此存储过程在发布服务器或订阅服务器上对任何数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>参数  
 [**@dbname=**] *****dbname*****  
 要设置其复制数据库选项的数据库。 *db_name*是**sysname**，无默认值。  
  
 [**@optname=**] *****optname*****  
 要启用或禁用的复制数据库选项。 *optname*是**sysname**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**合并发布**|数据库可用于合并发布。|  
|**发布**|数据库可用于其他类型的发布。|  
|**订阅**|数据库为订阅数据库。|  
|**与备份同步**|启用数据库以进行协调备份。 有关详细信息，请参阅[对于事务复制启用协调备份&#40;复制 TRANSACT-SQL 编程&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)。|  
  
 [  **@value=**] *****值*****  
 指示是启用还是禁用给定的复制数据库选项。 *值*是**sysname**，并且可以**true**或**false**。 当此值是**false**和*optname*是**合并发布**，也会删除对合并发布的数据库的订阅。  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 指示是否在未连接到分发服务器的情况下执行此存储过程。 *ignore_distributor*是**位**，默认值为**0**，这意味着分发服务器应连接到并与发布数据库的新状态更新。 值**1**应指定仅分发服务器是否无法访问和**sp_replicationdboption**用于禁用发布。  
  
 [  **@from_scripting=**] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replicationdboption**快照复制、 事务复制和合并复制中使用。  
  
 此过程根据给定的选项创建或删除特定的复制系统表、安全帐户，等等。 设置相应的类别中位**master.sysdatabases**系统表，然后创建必要的系统表。  
  
 若要禁用发布，发布数据库必须联机。 如果发布数据库存在数据库快照，则必须在禁用发布前将快照删除。 数据库快照是只读的脱机数据库的副本，并复制快照无关。 有关详细信息，请参阅[数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_replicationdboption**。  
  
## <a name="see-also"></a>另请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [删除发布](../../relational-databases/replication/publish/delete-a-publication.md)   
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
