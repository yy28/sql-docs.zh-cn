---
title: 新建全文非索引字表（"常规" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplist.general.f1
ms.assetid: 97f8e82d-82ab-4525-91c9-1ee3ae217309
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1dc58f006d1e37885418dfb923c6c7cc7563d018
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000827"
---
# <a name="new-full-text-stoplist-general-page"></a>新建全文非索引字表（“常规”页）
  使用此对话框可以创建全文非索引字表。 “非索引字表” ** 是一组称为“非索引字” ** 的常用字，在使用非索引字表的表的全文索引中会省略这些非索引字。 有关详细信息，请参阅 [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)。  
  
 **使用 SQL Server Management Studio 创建非索引字表**  
  
-   [为全文搜索配置和管理非索引字和非索引字表](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>选项  
 **全文非索引字表名称**  
 输入全文非索引字表的名称。  
  
 **所有者**  
 指定全文非索引字表的所有者。 如果希望将所有权分配给您自己（即分配给当前用户），请将此字段留空。  
  
 若要指定另一个用户，请单击浏览按钮。  
  
### <a name="create-stoplist-options"></a>创建非索引字表选项  
 单击下列创建选项之一：  
  
 **创建空非索引字表**  
 新非索引字表将不包含任何非索引字。  
  
 **从系统非索引字表创建**  
 用默认存在于 [资源数据库](../relational-databases/databases/resource-database.md)中的非索引字表创建新的非索引字表。  
  
 **从现有全文非索引字表创建**  
 通过复制现有的非索引字表来创建新的非索引字表。  
  
 **源数据库**  
 指定现有非索引字表所属的数据库的名称。 默认情况下选择当前数据库。 也可以从列表框中选择其他数据库。  
  
 **源非索引字表**  
 指定现有非索引字表的名称。 从可用非索引字表的列表中，选择一个要用作源的非索引字表。 可用非索引字表按照它们在对象资源管理器中显示的顺序列出。  
  
 如果源非索引字表的停止词中指定的任何语言未在当前数据库中注册，CREATE FULLTEXT STOPLIST 将成功，但会返回警告且不会添加相应的停止词。  
  
## <a name="see-also"></a>另请参阅  
 [更改全文非索引字表 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [创建全文非索引字表 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [删除全文非索引字表 &#40;Transact-sql&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)   
 [为全文搜索配置和管理非索引字和非索引字](../relational-databases/search/full-text-search.md)   
 [sys.fulltext_stoplists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
  
