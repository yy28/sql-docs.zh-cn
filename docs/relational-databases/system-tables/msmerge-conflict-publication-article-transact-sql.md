---
title: MSmerge_conflict_&lt;发布&gt;_&lt;文章(transact-sql)|&gt;Microsoft Docs
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
ms.openlocfilehash: 342b0f51fb4f68945f6ab8c4b511c5299acfba49
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893585"
---
# <a name="msmerge_conflict_ltpublicationgt_ltarticlegt-transact-sql"></a>MSmerge\_冲突\_发布&lt;文章(transact-sql&gt; )&gt;&lt;\_
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge\_冲突*发布*_文章表_包含有关发生冲突的行的信息, 以及为实现数据收敛而撤消的行更改的信息。\_\_** 对于发布中的每个复制表都存在一个冲突表，而冲突表的名称附加有发布和项目的名称。 这些项目特定的冲突表存储在用于进行冲突日志记录的数据库中，通常是发布数据库，但如果冲突日志记录分散，也可以是订阅数据库。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**_文章\_列\_名称_**|**variable**|表示复制表中的一列。 在该系统表中，表项目中的每列对应一列。|  
|**rowguid**|**uniqueidentifier**|冲突行的行标识符。|  
|ModifiedDate|**datetime**|发生冲突的时间。|  
|**源\_数据\_源 id**|**uniqueidentifier**|为其撤销行更改或失去冲突的订阅。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
