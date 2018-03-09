---
title: "ALTER BROKER 优先级 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 833c0bed38d02905b3a260f50824825c9859484f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 会话优先级的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>参数  
 *ConversationPriorityName*  
 指定要更改的会话优先级的名称。 名称必须引用当前数据库中的一个会话优先级。  
  
 SET  
 指定用于确定会话优先级是否应用于会话的条件。 SET 是必需的并且必须至少包含一个条件：CONTRACT_NAME、LOCAL_SERVICE_NAME、REMOTE_SERVICE_NAME 或 PRIORITY_LEVEL。  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 指定要用作会话优先级是否应用于会话的判定条件的约定的名称。 *ContractName*是[!INCLUDE[ssDE](../../includes/ssde-md.md)]标识符，并且必须在当前数据库中指定协定的名称。  
  
 *ContractName*  
 指定，可以仅对其中启动会话的 BEGIN DIALOG 语句指定 ON CONTRACT 会话应用会话优先级*ContractName*。  
  
 ANY  
 指定此会话优先级可应用于任何会话，而不考虑它使用的约定如何。  
  
 如果未指定 CONTRACT_NAME，则会话优先级的约定属性不会更改。  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 指定要用作确定会话优先级是否应用于会话端点的条件的服务名称。  
  
 *LocalServiceName*是[!INCLUDE[ssDE](../../includes/ssde-md.md)]标识符和必须在当前数据库中指定服务的名称。  
  
 *LocalServiceName*  
 指定此会话优先级可以应用于以下各项：  
  
-   发起方服务名称与匹配任何发起方会话端点*LocalServiceName*。  
  
-   其目标服务名称匹配任何目标会话端点*LocalServiceName*。  
  
 ANY  
 -   指定此会话优先级可应用于任何会话端点，而不管端点使用的本地服务的名称如何。  
  
 如果未指定 LOCAL_SERVICE_NAME，则会话优先级的本地服务属性不会更改。  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 指定要用作确定会话优先级是否应用于会话端点的条件的服务名称。  
  
 *RemoteServiceName*是类型的文字值**nvarchar(256)**。 [!INCLUDE[ssSB](../../includes/sssb-md.md)]使用逐字节比较，以匹配*RemoteServiceName*字符串。 这种比较区分大小写，并且不考虑当前的排序规则。 目标服务可以位于当前[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中，也可以位于远程[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中。  
  
 '*RemoteServiceName*'  
 指定将会话优先级分配给以下各项：  
  
-   相关联的目标服务名称与匹配任何发起方会话端点*RemoteServiceName*。  
  
-   其关联的发起程序服务名称匹配任何目标会话端点*RemoteServiceName*。  
  
 ANY  
 指定会话优先级应用于任何会话端点，而不管与端点关联的远程服务的名称如何。  
  
 如果未指定 REMOTE_SERVICE_NAME，则会话优先级的远程服务属性不会更改。  
  
 PRIORITY_LEVEL = { *PriorityValue* | **默认**}  
 指定要将使用的协定和服务中的会话优先级指定任何会话终结点分配的优先级级别。 *PriorityValue*必须是整数文本从 1 （最低优先级） 到 10 （最高优先级）。  
  
 如果未指定 PRIORITY_LEVEL，则会话优先级的优先级属性不会更改。  
  
## <a name="remarks"></a>注释  
 由 ALTER BROKER PRIORITY 更改的任何属性都不会应用于现有会话。 现有会话将继续使用启动时所分配的优先级。  
  
 有关详细信息，请参阅[CREATE BROKER PRIORITY &#40;Transact SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 权限创建的成员的默认值的会话优先级**db_ddladmin**或**db_owner**固定数据库角色的成员，并对其**sysadmin**固定的服务器角色。 需要对数据库拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. 只更改现有会话优先级的优先级。  
 更改优先级，但不更改约定、本地服务或远程服务属性。  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. 更改现有会话优先级的所有属性。  
 更改优先级、约定、本地服务和远程服务属性。  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建 BROKER 优先级 &#40;Transact SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [删除 BROKER 优先级 &#40;Transact SQL &#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
