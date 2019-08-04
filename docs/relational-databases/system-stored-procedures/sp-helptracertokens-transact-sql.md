---
title: sp_helptracertokens (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9b4df50d1cf43ba1b0f4eb8b8f313634b4d11d18
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771540"
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  为每个插入到发布以确定滞后时间的跟踪标记分别返回一行。 此存储过程在发布服务器上的发布数据库中执行，或者在分发服务器上的分发数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`在其中插入跟踪令牌的发布的名称。 *发布*为**sysname**, 无默认值。  
  
`[ @publisher = ] 'publisher'`发布服务器的名称。 *发布服务器*的**sysname**, 默认值为 NULL。  
  
> [!NOTE]
>  只应为非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器指定此参数。  
  
`[ @publisher_db = ] 'publisher_db'`发布数据库的名称。 *publisher_db*的值为**sysname**, 默认值为 NULL。 如果在发布服务器上执行该存储过程，将忽略此参数。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|标识跟踪令牌记录。|  
|**publisher_commit**|**datetime**|在发布服务器的发布数据库中提交标记记录的日期和时间。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 **sp_helptracertokens**用于事务复制。  
  
 **sp_helptracertokens**用于获取执行[ &#40;sp_helptracertokenhistory Transact-sql 时的&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)跟踪令牌 id。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员、发布数据库中的**db_owner**固定数据库角色的成员或分发数据库中的**db_owner**固定数据库或**replmonitor**角色的成员才能执行**sp_helptracertokenhistory**。  
  
## <a name="see-also"></a>请参阅  
 [为事务复制测量滞后时间和验证连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
