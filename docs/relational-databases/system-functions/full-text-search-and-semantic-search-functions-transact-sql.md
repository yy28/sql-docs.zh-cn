---
title: 全文搜索和语义搜索函数 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d8cccc6f36996808693e007e87ff1de7edfdd4a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105101"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>全文搜索和语义搜索函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节介绍与全文搜索以及语义搜索相关的系统函数。  
  
## <a name="full-text-search-functions"></a>全文搜索函数  
 [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)  
 返回由包含以下各项的列组成的零行、一行或多行表：单个词或短语的完全匹配项或模糊匹配项、词在一定差别范围内的相近或加权匹配项。  
  
 [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 返回的零个、 一个或多个行包含以下与匹配的含义，但不只是确切的措辞中指定的文本的值的列的表*freetext_string*。  
  
## <a name="semantic-search-functions"></a>语义搜索函数  
 [semantickeyphrasetable (Transact-SQL)](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 为与指定表中的列关联的那些关键短语返回包含零行、一行或多行的表。  
  
 [semanticsimilaritydetailstable (Transact-SQL)](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 返回一个表，该表包含内容在语义上相似的两个文档（源文档和匹配的文档）共有的零个、一个或多个关键短语行。  
  
 [semanticsimilaritytable (Transact-SQL)](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 为内容语义上类似于指定文档的列返回具有零个、一个或多个行的表。  
  
  
