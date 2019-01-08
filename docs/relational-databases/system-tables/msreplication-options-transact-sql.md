---
title: MSreplication_options (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4bb4c4568c220df16f9f5592f8e38d143340f96b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757939"
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_options**表存储在内部使用的复制元数据。 此表存储中**主**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|仅限内部使用。|  
|**value**|**bit**|仅限内部使用。|  
|**major_version**|**int**|仅限内部使用。|  
|**minor_version**|**int**|仅限内部使用。|  
|**修订版本**|**int**|仅限内部使用。|  
|**install_failures**|**int**|仅限内部使用。|  
  
## <a name="see-also"></a>请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
