---
title: "sp_requestpeerresponse (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords: sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d0a4009c5a6615a000989e2d41f2902ac37535f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从对等拓扑中的节点执行此过程时，此过程将从拓扑中的其他每个节点请求响应。 通过执行此过程并检查对应的响应，可以保证所有先前命令都已传递到响应的节点。 此存储过程在请求的节点上对任何数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication** =] *发布*  
 要验证其状态的对等拓扑中的发布名称。 *发布*是**sysname**，无默认值。  
  
 [  **@description** =] *说明*  
 可用于标识各个状态请求的用户定义信息。 *说明*是**nvarchar （4000)**，默认值为 NULL。  
  
 [  **@request_id**  =] *request_id*  
 返回新请求的 ID。 *request_id*是**int**和是一个输出参数。 在执行时，可以使用此值[sp_helppeerresponses &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)若要查看所有响应状态请求。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_requestpeerresponse**用于对等事务复制中。  
  
 **sp_requestpeerresponse**用于确保，所有命令都已由都接收的所有其他节点之前在对等拓扑中还原数据库发布。 此过程还用于复制节点脱机时所做的数据定义语言 (DDL) 更改，以评估这些更改到达其他节点的时间。  
  
 **sp_requestpeerresponse**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_requestpeerresponse**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_deletepeerrequesthistory &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
