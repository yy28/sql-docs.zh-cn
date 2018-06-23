---
title: 选择表和视图 （数据源视图向导） (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8bf3897fe2466b00c0346590147884696b632b7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027534"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>选择表和视图（数据源视图向导）(Analysis Services)
  可以使用 **“选择表和视图”** 页，从要包含在数据源视图中的数据源选择表或视图。  
  
## <a name="options"></a>“常规”  
 **可用对象**  
 在数据源架构中列出表和视图。 如果列出多个架构，则每个对象都以架构名称为前缀。 如果只列出一个架构，那么对象名称就不是以架构名称为前缀。  
  
 若要按照升序或降序顺序对列表重新排序，请单击 **“名称”** 或 **“类型”**。  
  
 **包括的对象**  
 列出要包含在数据源视图中的表和视图。  
  
 若要按照升序或降序顺序对列表重新排序，请单击 **“名称”** 或 **“类型”**。  
  
 **Filter**  
 筛选“可用对象”下列出的对象。 键入字符串，再单击 **“筛选器”** 以仅列出包含指定字符串的名称。 若要查找确切的字符串，请用双引号把字符串括起。 筛选器不区分大小写。  
  
 可以在筛选器字符串中的任意位置使用下表所列出的通配符：  
  
|通配符|ReplTest1|  
|------------------------|-----------|  
|**\***|任何字符串|  
|**%**|任何字符串|  
|**?**|单个字符|  
|**"** *string* **"**|文字字符串。 此通配符将与对象名称中的任何子字符串相匹配。|  
  
 **显示系统对象**  
 显示“可用对象”下的系统对象。 只有在数据源提供程序显示系统对象时，此选项才可用。 从 **“包含的对象”** 列表中删除系统对象时，将自动选择此项。  
  
 **添加相关的表**  
 添加与“包含的对象”下所列表相关的所有表。 此选项不能添加视图。 不过，此选项可以添加分区表。 如果在向导的“名称匹配”页选择名称匹配条件，则此选项还将根据所选条件包括逻辑相关表。 如果表与新添加的相关表有关，并与原始表具有相同结构，那么也会添加该表。  
  
## <a name="see-also"></a>请参阅  
 [数据源视图向导的 F1 帮助&#40;Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [多维模型中的数据源视图](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  