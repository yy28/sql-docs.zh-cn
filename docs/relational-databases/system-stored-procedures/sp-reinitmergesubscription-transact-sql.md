---
title: sp_reinitmergesubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b42439c35eaf2b240222987f577c8664263d657
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820321"
---
# <a name="sp_reinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将合并订阅标记为在下次运行合并代理时重新初始化。 此存储过程可在发布服务器的任意发布数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，默认值为**all**。  
  
`[ @subscriber = ] 'subscriber'`订阅服务器的名称。 *订阅服务器*的值为**sysname**，默认值为**all**。  
  
`[ @subscriber_db = ] 'subscriber_db'`订阅服务器数据库的名称。 *subscriber_db*的值为**sysname**，默认值为**all**。  
  
`[ @upload_first = ] 'upload_first'`在重新初始化订阅之前是否上载订阅服务器上的更改。 *upload_first*为**nvarchar （5）**，默认值为 FALSE。 如果**为 true**，则在重新初始化订阅之前上载更改。 如果**为 false**，则不上载更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_reinitmergesubscription**用于合并复制。  
  
 可从发布服务器调用**sp_reinitmergesubscription**以重新初始化合并订阅。 建议同时重新运行快照代理。  
  
 如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_reinitmergesubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
