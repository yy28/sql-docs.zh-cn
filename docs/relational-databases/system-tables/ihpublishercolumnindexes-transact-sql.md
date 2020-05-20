---
title: IHpublishercolumnindexes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fe01417988e21951722b7dbe5e1716cb13abe866
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832411"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnindexes**系统表将[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系统表中非 SQL Server 发布的列映射到[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)系统表中的索引。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|使用关联索引标识[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)中的列。|  
|**publisherindex_id**|**int**|标识与列关联的[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)表中的索引。|  
|**indid**|**int**|指示列在已发布表中的位置。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
