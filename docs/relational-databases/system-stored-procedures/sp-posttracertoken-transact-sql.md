---
title: sp_posttracertoken (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedur+I741es
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0076b5d48f329aaa5986c08a8a4396598607017
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030365"
---
# <a name="spposttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此过程将跟踪令牌发布到发布服务器上的事务日志，并开始跟踪滞后时间统计信息的过程。 如果将跟踪令牌写入了事务日志，则当日志读取器代理选中该令牌，以及分发代理应用该令牌时，均会记录信息。 在发布服务器上对发布数据库执行此存储的过程。 有关详细信息，请参阅 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>参数  
 [ **@publication**=] **'***发布*****  
 要测量滞后时间的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@tracer_token_id=** ] *tracer_token_id * * * 输出**  
 插入的跟踪令牌的 ID。 *tracer_token_id*是**int** ，默认值为 NULL，它是一个输出参数。 此值可用于执行[sp_helptracertokenhistory &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)或[sp_deletetracertokenhistory &#40;-&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)而不用先执行[sp_helptracertokens &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)。  
  
 [  **@publisher=** ] **'***发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL，不应指定为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_posttracertoken**事务复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_posttracertoken**。  
  
## <a name="see-also"></a>请参阅  
 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
