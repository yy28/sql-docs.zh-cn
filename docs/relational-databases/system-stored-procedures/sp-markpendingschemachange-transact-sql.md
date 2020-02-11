---
title: sp_markpendingschemachange （Transact-sql） |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56ed176d8b4b29e1ed4caafabd0893b7a33b1293
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73962395"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @schemaversion = ] schemaversion`标识挂起的架构更改。 *schemaversion*为**int**，默认值为**0**。 使用[sp_enumeratependingschemachanges &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md)列出发布的挂起的架构更改。  
  
`[ @status = ] 'status'`是否将跳过挂起的架构更改。 *状态*为**nvarchar （10）** ，默认值为 "**活动**"。 如果**跳过***状态*值，则不会复制所选的架构更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_markpendingschemachange**用于合并复制。  
  
 **sp_markpendingschemachange**是一种用于合并复制的可支持性的存储过程，只应在其他纠正措施（如重新初始化）无法纠正这种情况或在性能方面过于昂贵时使用。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_markpendingschemachange**。  
  
## <a name="see-also"></a>另请参阅  
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
