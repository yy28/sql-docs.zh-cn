---
title: sp_posttracertoken （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7629c25264f0b45d68e29e947b1d5c40d02707e7
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041180"
---
# <a name="sp_posttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此过程将跟踪令牌发布到发布服务器上的事务日志，并开始跟踪滞后时间统计信息的过程。 如果将跟踪令牌写入了事务日志，则当日志读取器代理选中该令牌，以及分发代理应用该令牌时，均会记录信息。 此存储过程在发布服务器上对发布数据库执行。 有关详细信息，请参阅 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是要测量其滞后时间的发布的名称。 *发布*为**sysname**，无默认值。  
  
@no__t 为插入的跟踪令牌的 ID。 *tracer_token_id*的默认值为**int** ，默认值为 NULL，它是一个 OUTPUT 参数。 此值可用于在不首先[执行&#40;&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md) sp_helptracertokens [ &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md) [ &#40;transact-sql 的情况下执行 sp_helptracertokenhistory transact-sql 或 sp_deletetracertokenhistory transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md).  
  
@no__t 指定一个非 @no__t 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*的**sysname**为，默认值为 NULL，不应为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_posttracertoken**用于事务复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_posttracertoken**。  
  
## <a name="see-also"></a>请参阅  
 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
