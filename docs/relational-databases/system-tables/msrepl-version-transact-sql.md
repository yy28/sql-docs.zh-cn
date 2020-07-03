---
title: MSrepl_version （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_version
- MSrepl_version_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_version system table
ms.assetid: c1330f03-940b-4564-ac42-6030c6e21173
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3176da347195e7410c5062a442c7f1d5b5881791
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889475"
---
# <a name="msrepl_version-transact-sql"></a>MSrepl_version (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_version**表中包含一个已安装复制的当前版本的行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**major_version**|**int**|分发数据库的主版本号。|  
|**minor_version**|**int**|分发数据库的次版本号。|  
|**a01**|**int**|修订号。|  
|**db_existed**|**bit**|指示在调用**sp_adddistributiondb**之前分发数据库是否存在。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
