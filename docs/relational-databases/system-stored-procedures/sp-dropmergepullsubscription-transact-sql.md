---
title: "用 sp_dropmergepullsubscription (Transact SQL) |Microsoft 文档"
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
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20bae9a8d1a27e0ec4a02a6cb3dc632fa50924ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除合并请求订阅。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。 此参数是必需的。 指定的值**所有**若要删除所有发布的订阅  
  
 [  **@publisher=**] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 此参数是必需的。  
  
 [  **@publisher_db=**] *publisher_db*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 此参数是必需的。  
  
 [  **@reserved=**] *保留*  
 供将来使用的保留参数。 *保留*是**位**，默认值为**0**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **用 sp_dropmergepullsubscription**合并复制中使用。  
  
 **用 sp_dropmergepullsubscription**删除此合并请求订阅，合并代理，尽管合并代理未以创建**sp_addmergepullsubscription**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或创建合并请求订阅的用户可以执行**用 sp_dropmergepullsubscription**。 **Db_owner**固定的数据库角色是否只能执行**用 sp_dropmergepullsubscription**如果创建合并请求订阅的用户属于此角色。  
  
## <a name="see-also"></a>另请参阅  
 [删除请求订阅](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
