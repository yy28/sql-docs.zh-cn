---
title: MSmerge_conflict_&lt;出版物&gt;_&lt;一文&gt;(TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78036e91dd87b3295c9b8c4e6d0a39311133bbdd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777949"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>MSmerge_conflict_&lt;出版物&gt;_&lt;一文&gt;(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflict_*发布*_ * 文章*** 表包含在发生冲突的行上或针对实现数据收敛而撤消的行更改的信息。 对于发布中的每个复制表都存在一个冲突表，而冲突表的名称附加有发布和项目的名称。 这些项目特定的冲突表存储在用于进行冲突日志记录的数据库中，通常是发布数据库，但如果冲突日志记录分散，也可以是订阅数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|***article_column_name***|variable|表示复制表中的一列。 在该系统表中，表项目中的每列对应一列。|  
|**rowguid**|**uniqueidentifier**|冲突行的行标识符。|  
|ModifiedDate|**datetime**|发生冲突的时间。|  
|**origin_datasource_id**|**uniqueidentifier**|为其撤销行更改或失去冲突的订阅。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
