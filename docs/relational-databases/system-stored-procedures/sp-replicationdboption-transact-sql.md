---
title: sp_replicationdboption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8285713df1fb17b2e82dcfa6edac0fd6db5500a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950664"
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
 [ **@dbname=** ] **'***dbname***’**  
 要设置其复制数据库选项的数据库。 *db_name*是**sysname**，无默认值。  
  
 [ **@optname=** ] **'***optname***’**  
 要启用或禁用的复制数据库选项。 *optname*是**sysname**，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**合并发布**|数据库可用于合并发布。|  
|**publish**|数据库可用于其他类型的发布。|  
|**subscribe**|数据库为订阅数据库。|  
|**与备份同步**|启用数据库以进行协调备份。 有关详细信息，请参阅[为事务复制启用协调备份&#40;复制 TRANSACT-SQL 编程&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)。|  
  
`[ @value = ] 'value'` 要启用或禁用给定的复制数据库选项。 *值*是**sysname**，并且可以**true**或**false**。 当此值是**false**并*optname*是**合并发布**，还将删除对合并发布数据库的订阅。  
  
`[ @ignore_distributor = ] ignore_distributor` 指示是否无需连接到分发服务器上执行此存储的过程。 *ignore_distributor*是**位**，默认值为**0**，表示分发服务器应连接到并使用发布数据库的新状态更新。 该值**1**应仅在指定分发服务器是无法访问并**sp_replicationdboption**用于禁用发布。  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_replicationdboption**快照复制、 事务复制和合并复制中使用。  
  
 此过程根据给定的选项创建或删除特定的复制系统表、安全帐户，等等。 设置相应的类别中的位**master.sysdatabases**系统表，并创建必要的系统表。  
  
 若要禁用发布，发布数据库必须联机。 如果发布数据库存在数据库快照，则必须在禁用发布前将快照删除。 数据库快照的数据库的只读脱机副本，并与复制快照无关。 有关详细信息，请参阅[数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_replicationdboption**。  
  
## <a name="see-also"></a>请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [删除发布](../../relational-databases/replication/publish/delete-a-publication.md)   
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
