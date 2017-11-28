---
title: "ALTER SERVICE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69756a85873ddae09780e28b2ccc5481659e563f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改现有的服务。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  
## <a name="arguments"></a>参数  
 *service_name*  
 要更改的服务的名称。 不能指定服务器、数据库和架构名称。  
  
 ON 队列 [ *schema_name***。** ] *queue_name*  
 为此服务指定新队列。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将此服务的所有消息从当前队列移动到新队列。  
  
 添加协定*contract_name*  
 指定要添加到由此服务公开的约定集中的约定。  
  
 删除协定*contract_name*  
 指定要从由此服务公开的约定集中删除的约定。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 将对使用该约定的、与此服务进行的所有现有会话发送错误消息。  
  
## <a name="remarks"></a>注释  
 当 ALTER SERVICE 语句从某个服务中删除一条约定后，此服务便不可再作为使用该约定的会话的目标。 因此，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 将不允许使用该约定与此服务建立新会话。 使用该约定的现有会话不受影响。  
  
 若要更改服务的 AUTHORIZATION，请使用 ALTER AUTHORIZATION 语句。  
  
## <a name="permissions"></a>Permissions  
 更改服务的权限默认为服务的成员的所有者**db_ddladmin**或**db_owner**固定数据库角色和成员的**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. 更改服务队列  
 下面的示例将 `//Adventure-Works.com/Expenses` 服务更改为使用队列 `NewQueue`。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. 向服务中添加新约定  
 下面的示例将 `//Adventure-Works.com/Expenses` 服务更改为允许在 `//Adventure-Works.com/Expenses` 约定上进行对话。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. 向此服务中添加新约定，并删除现有约定  
 下面的示例将 `//Adventure-Works.com/Expenses` 服务更改为允许在 `//Adventure-Works.com/Expenses/ExpenseProcessing` 约定上进行对话，而不允许在 `//Adventure-Works.com/Expenses/ExpenseSubmission` 约定上进行对话。  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SERVICE (Transact SQL)](../../t-sql/statements/create-service-transact-sql.md)   
 [删除服务 &#40;Transact SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
