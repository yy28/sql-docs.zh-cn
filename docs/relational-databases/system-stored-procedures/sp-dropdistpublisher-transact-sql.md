---
title: "sp_dropdistpublisher (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8060e5788004b743e58e0d0d424dcc0910459573
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除分发发布服务器。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=** ] *发布服务器*  
 要删除的发布服务器。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@no_checks=** ] *no_checks*  
 指定是否**sp_dropdistpublisher**检查发布服务器已卸载作为分发服务器的服务器。 *no_checks*是**位**，默认值为**0**。  
  
 如果**0**，复制验证远程发布服务器已卸载本地服务器作为分发服务器。 如果发布服务器是本地服务器，则复制将验证没有发布对象或分发对象保留在本地服务器上。  
  
 如果**1**，即使无法访问远程发布服务器删除分发发布服务器与关联的所有复制对象。 执行此操作后，远程发布服务器必须卸载复制使用[sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)与 **@ignore_distributor**   =  **1**。  
  
 [  **@ignore_distributor=** ] *ignore_distributor*  
 指定删除发布服务器时是否将分发对象保留在分发服务器中。 *ignore_distributor*是**位**和可以是下列值之一：  
  
 **1** = 分发对象属于*发布服务器*始终在分发服务器。  
  
 **0** = 分发对象*发布服务器*是已清理的分发服务器上。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_dropdistpublisher**在所有类型的复制中使用。  
  
 删除 Oracle 发布服务器，如果无法删除发布服务器时**sp_dropdistpublisher**返回删除错误发布服务器的分发服务器对象。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_dropdistpublisher**。  
  
## <a name="see-also"></a>另请参阅  
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
