---
title: MSpublication_access （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublication_access_TSQL
- MSpublication_access
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublication_access system table
ms.assetid: 7bebe47e-3153-4579-8092-5723667a24c6
author: stevestein
ms.author: sstein
ms.openlocfilehash: fccf3e82fbf5958e0293c462961d8aa9b459e594
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947779"
---
# <a name="mspublication_access-transact-sql"></a>MSpublication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于**** 每个[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有权访问特定发布或发布服务器的登录名，MSpublication_access 表都包含一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|发布 ID。|  
|**id**|**sysname**|同时存在于发布服务器和分发服务器端的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
