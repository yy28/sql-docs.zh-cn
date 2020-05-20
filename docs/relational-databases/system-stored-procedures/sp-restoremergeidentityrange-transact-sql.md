---
title: sp_restoremergeidentityrange （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a41b725d46c96f1ab79444246ab538b0c3f539f0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816868"
---
# <a name="sp_restoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程用于更新标识范围分配。 该存储过程可确保从备份还原发布服务器后，自动标识范围管理运行正常。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，默认值为**all**。 如果指定了此参数，则只还原该发布的标识范围。  
  
`[ @article = ] 'article'`项目的名称。 *项目*的值为**sysname**，默认值为**all**。 如果指定了此参数，则只还原该项目的标识范围。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_restoremergeidentityrange**用于合并复制。  
  
 **sp_restoremergeidentityrange**从分发服务器获取最大标识范围分配信息，并更新使用自动标识范围管理的项目[MSmerge_identity_range_allocations &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md)的**max_used**列中的值。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_restoremergeidentityrange**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
