---
title: IHpublishercolumnconstraints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7f6c4b609159d34c1159a248c8ea9a9eacc24d18
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813457"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnconstraints**系统表将[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系统表中非 SQL Server 发布的列映射到[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)系统表中的约束。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|使用关联的约束标识[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)中的列。|  
|**publisherconstraint_id**|**int**|标识与列关联的[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)的约束。|  
|**indid**|**int**|指示列在已发布表中的位置。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
