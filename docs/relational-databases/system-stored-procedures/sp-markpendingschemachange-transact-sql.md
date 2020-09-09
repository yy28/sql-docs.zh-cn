---
description: sp_markpendingschemachange (Transact-SQL)
title: sp_markpendingschemachange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b5b207c4d36e820e6635bd9c8a2e99cdb7e4829
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541687"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  用于合并发布的可支持性，它通过让管理员跳过所选的挂起架构更改，不复制这些更改。 此存储过程在发布服务器上对发布数据库执行。  
  
> [!CAUTION]  
>  此存储过程可以导致架构更改不被复制。 只有在尝试了其他方法（例如，重新初始化）之后，或者这些方法的性能开销太大，才用此过程来解决问题。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 发布的名称。 *发布* 为 **sysname**，无默认值。  
  
`[ @schemaversion = ] schemaversion` 标识挂起的架构更改。 *schemaversion* 为 **int**，默认值为 **0**。 使用 [sp_enumeratependingschemachanges &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) 列出发布的挂起的架构更改。  
  
`[ @status = ] 'status'` 是否将跳过挂起的架构更改。 *状态* 为 **nvarchar (10) ** ，默认值为 " **活动**"。 如果**跳过***状态*值，则不会复制所选的架构更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 **sp_markpendingschemachange** 用于合并复制。  
  
 **sp_markpendingschemachange** 是一种用于合并复制的可支持性的存储过程，只应在其他纠正措施（如重新初始化）无法纠正这种情况或在性能方面过于昂贵时使用。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员或 **db_owner** 固定数据库角色的成员才能执行 **sp_markpendingschemachange**。  
  
## <a name="see-also"></a>另请参阅  
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
