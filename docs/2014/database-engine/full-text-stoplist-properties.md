---
title: 全文非索引字表属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4cfdd308ab7488633721ddaac55d3d926a276b0d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779404"
---
# <a name="full-text-stoplist-properties"></a>全文非索引字表属性
  使用该对话框可以添加或删除单个非索引字、删除特定语言的所有非索引字或者清除当前的非索引字表。 非索引字是指包括在非索引字表中的常用字。 非索引字表中的非索引字将从使用非索引字表的表的全文索引中省略。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)。  
  
 **使用 SQL Server Management Studio 更改非索引字表属性**  
  
-   [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>选项  
 **操作**  
 指定要执行的操作。  
  
 **添加非索引字**  
 向非索引字表中添加常用字。  
  
 **删除非索引字**  
 从非索引字表中删除非索引字。  
  
 **删除所有非索引字**  
 删除特定语言的所有非索引字。  
  
 **清除非索引字表**  
 通过删除所有语言的全部非索引字来清除非索引字表。  
  
 **非索引字**  
 如果您选择的是 **“添加非索引字”** 或 **“删除非索引字”**，请在 **“非索引字”** 字段中输入所需的非索引字。 新的非索引字必须是唯一的，也就是说，在针对所选语言的此非索引字表中还不存在该非索引字。  
  
 **全文语言**  
 如果您选择的是 **“添加非索引字”**、 **“删除非索引字”** 或 **“删除所有非索引字”**，请从列表框中选择非索引字的语言。 这将列出该服务器实例支持的所有全文语言。  
  
## <a name="see-also"></a>另请参阅  
 [sys. fulltext_stopwords &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys. fulltext_stoplists &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [为全文搜索配置和管理非索引字和非索引字](../relational-databases/search/full-text-search.md)   
 [更改全文非索引字表 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [创建全文非索引字表 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
