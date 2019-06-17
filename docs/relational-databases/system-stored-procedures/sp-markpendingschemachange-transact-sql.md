---
title: sp_markpendingschemachange (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 67377f638459a37f25fbc78b9acff395192a2f3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628260"
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于合并发布的可支持性，它通过让管理员跳过所选的挂起架构更改，不复制这些更改。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!CAUTION]  
>  此存储过程可以导致架构更改不被复制。 只有在尝试了其他方法（例如，重新初始化）之后，或者这些方法的性能开销太大，才用此过程来解决问题。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @schemaversion = ] schemaversion` 标识挂起的架构更改。 *schemaversion*是**int**，默认值为**0**。 使用[sp_enumeratependingschemachanges &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md)若要列出该发布的挂起的架构更改。  
  
`[ @status = ] 'status'` 是否跳过挂起的架构更改。 *状态*是**nvarchar(10)** 默认值为**active**。 如果的值*状态*是**跳过**，则将不会复制所选的架构更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_markpendingschemachange**与合并复制一起使用。  
  
 **sp_markpendingschemachange**是存储的过程可支持性的合并复制，仅当其他纠正操作，例如，重新初始化，无法更正这种情况，或在开销太大时，才应使用性能的条款。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_markpendingschemachange**。  
  
## <a name="see-also"></a>请参阅  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
