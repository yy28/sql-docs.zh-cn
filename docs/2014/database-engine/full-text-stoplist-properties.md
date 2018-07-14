---
title: 全文非索引字表属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 3802396c3b2ff6d64aa439af07e7dba2f9b30c60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241287"
---
# <a name="full-text-stoplist-properties"></a>全文非索引字表属性
  使用该对话框可以添加或删除单个非索引字、删除特定语言的所有非索引字或者清除当前的非索引字表。 非索引字是指包括在非索引字表中的常用字。 非索引字表中的非索引字将从使用非索引字表的表的全文索引中省略。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)。  
  
 **若要使用 SQL Server Management Studio 更改非索引字表属性**  
  
-   [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>“常规”  
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
  
## <a name="see-also"></a>请参阅  
 [sys.fulltext_stopwords (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys.fulltext_stoplists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
