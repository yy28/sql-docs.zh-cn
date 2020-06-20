---
title: 全文目录属性（"表和视图" 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: rothja
ms.author: jroth
ms.openlocfilehash: eb4d968af6c550d19fbb8934b5d76a1bd63cb8da
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933008"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>全文目录属性（“表和视图”页）
  使用此对话框可以查看或修改为全文目录分配的表和视图。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 **此数据库中所有合格的表/视图对象**  
 列出对其定义了唯一索引、但并未包含在全文目录中的表和视图。 若要选择某个表或视图并将其分配给目录，请在列表框中选择相应的项，然后按 "->" 按钮。  
  
 **分配给该目录的表/视图对象**  
 列出当前分配给全文目录的表和视图。  
  
## <a name="selected-object-properties"></a>所选对象属性  
 **所选对象属性**  
 显示在分配给该目录的对象的列表框中所选对象的属性。  
  
 **唯一索引**  
 列出表或视图可用的唯一索引。  
  
 **表支持全文索引**  
 若要对该表启用全文索引，请选中此复选框。 若要禁用全文索引，请清除此复选框。  
  
## <a name="eligible-columns-grid"></a>“合格列”网格  
  
|||  
|-|-|  
|**可用列**|显示进行全文索引的所有列。 若要向全文索引中添加列，请选中相应的复选框。|  
|**断字符语言**|显示断字符的语言。|  
|**数据类型列**|列出表中列的名称，该列包含在 "**可用列**" 中列出的列的文档类型（如果该列是 `varbinary(max)` 或 `image` 列）。|  
|**统计语义**|选择是否为所选列启用语义索引。 有关详细信息，请参阅[语义搜索 (SQL Server)](../relational-databases/search/semantic-search-sql-server.md)。<br /><br /> 如果您在选择 **“统计语义”** 前选择某一 **“语言”**，并且所选语言没有关联的语义语言模型，则 **“统计语义”** 复选框将被禁用。 如果你在选择****“语言”前选择****“统计语义”，则下拉组合框中提供的语言将限制为存在语义语言模型支持的那些语言。|  
  
## <a name="track-changes"></a>跟踪更改  
  
|||  
|-|-|  
|**自动**|在修改、添加或删除基础表中的数据时，将自动更新全文索引。|  
|**手动**|在修改、添加或删除索引数据中的数据时， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将跟踪所做的更改。 当 **“手动”** 更改跟踪处于有效状态时，不会使用这些更改自动更新索引。 相反，管理员可以使用 [ALTER FULLTEXT INDEX ...START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql) 语句手动应用更改。|  
|**不跟踪更改**|如果此选项处于有效状态，则不会记录对目录中索引数据所做的更改。 管理员必须将 ALTER FULLTEXT INDEX 与 FULL POPULATION 或 INCREMENTAL POPULATION 一起使用以生成索引。|  
  
## <a name="see-also"></a>另请参阅  
 [CREATE FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [&#40;Transact-sql&#41;更改全文目录](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [填充全文索引](../relational-databases/indexes/indexes.md)  
  
  
