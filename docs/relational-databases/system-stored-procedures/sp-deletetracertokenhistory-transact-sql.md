---
title: sp_deletetracertokenhistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f84cd1cbb9a49f0c13a93fdff721f430983088ca
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955968"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

删除跟踪令牌记录从[MStracer_tokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)并[MStracer_history &#40;-&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md)系统表。 此存储过程在发布服务器上的发布数据库中执行，或者在分发服务器上的分发数据库中执行。

![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>语法

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>参数

`@publication= 'publication'`  
已插入跟踪令牌的发布的名称。 数据类型是**sysname**。 此参数是必需的。

`[ @tracer_id= ] tracer_id`  
要删除的跟踪令牌的 ID。 数据类型是**int**。默认值为 null。 如果*null*，会删除属于该发布的所有跟踪令牌。

`[ @cutoff_date= ] cutoff_date`  
删除此日期之前插入到发布的跟踪令牌。 数据类型是**datetime**。 默认值为 null。

`[ @publisher= ] 'publisher'`  
发布服务器的名称。 数据类型是**sysname**。 默认值为 null。

> [!NOTE]
> 应仅指定此参数为非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器或从分发服务器上执行存储的过程时。

`[ @publisher_db= ] 'publisher_db'`  
发布数据库的名称。 数据类型是**sysname**。 默认值为 NULL。 如果在发布服务器上执行该存储过程，将忽略此参数。

> [!NOTE]
> 从分发服务器上执行存储的过程时，应指定此参数。

## <a name="return-code-values"></a>返回代码值

**0** （成功） 或**1** （失败）

## <a name="remarks"></a>备注

**sp_deletetracertokenhistory**事务复制中使用。  

如果未指定这两个参数，就会出错*tracer_id*并*cutoff_date*。

如果不执行**sp_deletetracertokenhistory**若要删除跟踪令牌元数据，信息将被删除时定期计划的历史记录清除执行。

可通过执行确定跟踪令牌 Id [sp_helptracertokens &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)或通过查询[MStracer_tokens &#40;-&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)系统表。

## <a name="permissions"></a>权限

只有以下人员有权执行**sp_deletetracertokenhistory**:

- 成员**replmonitor**分发数据库中的角色
- 成员**sysadmin**固定的服务器角色。
- 成员**db_owner**固定的数据库角色，对发布数据库中。
- **Db_owner**的固定的数据库。

## <a name="see-also"></a>请参阅

[为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
