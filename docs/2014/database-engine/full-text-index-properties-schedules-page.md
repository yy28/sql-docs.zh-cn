---
title: 全文本索引属性 （计划页） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e564784e5f3fcae652068dcb200a805062a5e6bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026829"
---
# <a name="full-text-index-properties-schedules-page"></a>全文索引属性（“计划”页）
  使用此页可以查看和创建运行 SQL Server 代理作业的计划，该作业用于启动对全文索引基表的更新的增量填充。 如果基表或视图不包含的列`timestamp`数据类型，则执行完全填充。  
  
 **若要查看或更改全文索引的属性**  
  
-   [管理全文检索](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>UIElement 列表  
 **计划**  
 列出全文索引的基表上的每个计划增量填充（如果有）。  
  
 **名称**  
 显示每个计划填充的名称。  
  
 **填充类型**  
 显示每个计划填充的类型。  
  
 **已启用**  
 指示当前是启用还是禁用计划填充。  
  
 **Description**  
 显示创建计划时指定的说明。  
  
 **新建**  
 单击此选项可以为填充全文索引创建新计划。  
  
## <a name="see-also"></a>请参阅  
 [使用全文索引向导](../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [填充全文索引](../relational-databases/search/populate-full-text-indexes.md)  
  
  