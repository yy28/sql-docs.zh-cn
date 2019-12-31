---
title: MSmerge_conflict_publication_article （T-sql）
description: 介绍 MSmerge_conflict_publication_article 存储过程，该存储过程包含有关发生冲突的行的信息，或者为实现数据收敛而撤消的行更改。
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 8d2c324f032f9cdd3206f6f2bed77fba74c2c0f5
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322108"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflict_publication_article**表包含有关发生冲突的行的信息，或者为实现数据收敛而撤消的行更改的信息。 对于发布中的每个复制表都存在一个冲突表，而冲突表的名称附加有发布和项目的名称。 这些项目特定的冲突表存储在用于进行冲突日志记录的数据库中，通常是发布数据库，但如果冲突日志记录分散，也可以是订阅数据库。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**_文章\_列\_名称_**|**各种**|表示复制表中的一列。 在该系统表中，表项目中的每列对应一列。|  
|**rowguid**|**uniqueidentifier**|冲突行的行标识符。|  
|**ModifiedDate**|**型**|发生冲突的时间。|  
|**源\_数据\_源 id**|**uniqueidentifier**|为其撤销行更改或失去冲突的订阅。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
