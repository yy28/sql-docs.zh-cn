---
title: 全文本索引属性 （列页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 67b7e72e0c4b248e8951667561eaf7548bfba1b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778852"
---
# <a name="full-text-index-properties-columns-page"></a>全文索引属性（“列”页）
  **若要查看或更改全文索引的属性**  
  
-   [管理全文检索](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>UIElement 列表  
 **唯一索引**  
 从下拉列表中选择索引。 索引必须是唯一且不为 Null 的单键列索引。  
  
 **选择将为全文索引的合格列**  
 此网格显示可用于此全文索引的表列。 已选中当前是全文索引的列。 或者，可以选中要成为全文索引的其他列。  
  
> [!IMPORTANT]  
>  在单击“确定”之前，请确保至少选中一列。  
  
|||  
|-|-|  
|**可用列**|列名称。|  
|**断字符语言**|其断字符和词干分析器对所有全文索引数据执行语言分析的语言。<br /><br /> 有关详细信息，请参阅[配置和管理断字符和词干分析器以便搜索](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)并[语言创建时选择全文索引](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。|  
|**类型**|保留所选列的文档类型的表列的名称。 此属性是只读属性。|  
|**统计语义**|选择是否为所选列启用语义索引。 有关详细信息，请参阅[语义搜索 (SQL Server)](../relational-databases/search/semantic-search-sql-server.md)。<br /><br /> 如果您在选择 **“统计语义”** 前选择某一 **“语言”**，并且所选语言没有关联的语义语言模型，则 **“统计语义”** 复选框将被禁用。 如果你在选择“语言”前选择“统计语义”，则下拉组合框中提供的语言将限制为存在语义语言模型支持的那些语言。|  
  
## <a name="see-also"></a>请参阅  
 [填充全文索引](../relational-databases/search/populate-full-text-indexes.md)  
  
  
