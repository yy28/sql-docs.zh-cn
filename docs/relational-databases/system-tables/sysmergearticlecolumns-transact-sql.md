---
title: sysmergearticlecolumns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergearticlecolumns
- sysmergearticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticlecolumns system table
ms.assetid: 1ad8663f-a624-42a2-8641-fefac3433c97
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2edf9a5656eaf9dd3f18adff28562e279db892e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029961"
---
# <a name="sysmergearticlecolumns-transact-sql"></a>sysmergearticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergearticlecolumns**表包含每个表列的合并发布中发布，并将每个列映射到其合并项目占一行。 该表存储在发布数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|标识项目。|  
|**列 id**|**smallint**|标识项目中的列。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
