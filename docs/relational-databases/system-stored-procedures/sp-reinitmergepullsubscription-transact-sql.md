---
title: sp_reinitmergepullsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c6e5dc234cdba7608faa4f2ad8693918f59ad7f8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645883"
---
# <a name="sp_reinitmergepullsubscription-transact-sql"></a>sp_reinitmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  将合并请求订阅标记为在下次运行合并代理时重新初始化。 此存储过程在订阅服务器上针对订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_reinitmergepullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>自变量  
`[ @publisher = ] 'publisher'`发布服务器的名称。 *发布服务器*的**sysname**，默认值为 ALL。  
  
`[ @publisher_db = ] 'publisher_db'`发布服务器数据库的名称。 *publisher_db*的值为**sysname**，默认值为 ALL。  
  
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，默认值为 ALL。  
  
`[ @upload_first = ] 'upload_first'`在重新初始化订阅之前是否上载订阅服务器上的更改。 *upload_first*为**nvarchar （5）**，默认值为 FALSE。 如果**为 true**，则在重新初始化订阅之前上载更改。 如果**为 false**，则不上载更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_reinitmergepullsubscription**用于合并复制。  
  
 如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_reinitmergepullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_1.sql)]  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_reinitmergepullsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_2.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_reinitmergepullsubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [重新初始化订阅](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
