---
title: 全文搜索和语义搜索函数（Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 58bf5650a5ab06783ad0c889bc3286184a7d73ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68042753"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>全文搜索和语义搜索函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本节介绍与全文搜索以及语义搜索相关的系统函数。  
  
## <a name="full-text-search-functions"></a>全文搜索函数  
 [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)  
 返回由包含以下各项的列组成的零行、一行或多行表：单个词或短语的完全匹配项或模糊匹配项、词在一定差别范围内的相近或加权匹配项。  
  
 [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 返回一个表，其中包含与指定的*freetext_string*中的文本匹配的值（而不只是精确的文字）的行、一行或多行。  
  
## <a name="semantic-search-functions"></a>语义搜索函数  
 [semantickeyphrasetable (Transact-SQL)](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 为与指定表中的列关联的那些关键短语返回包含零行、一行或多行的表。  
  
 [semanticsimilaritydetailstable (Transact-SQL)](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 返回一个表，该表包含内容在语义上相似的两个文档（源文档和匹配的文档）共有的零个、一个或多个关键短语行。  
  
 [semanticsimilaritytable (Transact-SQL)](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 为内容语义上类似于指定文档的列返回具有零个、一个或多个行的表。  
  
  
