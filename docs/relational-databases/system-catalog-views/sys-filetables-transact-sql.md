---
title: sys.filetables (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fff9e99a6e7fbd9e6e2e9490d8b67fce75586b6e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038338"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的每个 FileTable 返回一行。 有关 FileTable 的详细信息，请参阅 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。    
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**||对象标识号。 是在数据库中唯一。<br /><br /> 有关详细信息[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_enabled**|**bit**|1 = FileTable 处于“已启用”状态。|  
|**directory_name**|**varchar(255)**|FileTable 的根目录名称。|  
|**filename_collation_id**||为 FileTable 定义的排序规则标识符|  
|**filename_collation_name**||为 FileTable 定义的排序规则名称。|  
  
## <a name="see-also"></a>请参阅  
 [管理 Filetable](../../relational-databases/blob/manage-filetables.md)   
 [FileTables (SQL Server)](../../relational-databases/blob/filetables-sql-server.md)  
  
  
