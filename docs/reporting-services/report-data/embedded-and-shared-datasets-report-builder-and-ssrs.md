---
title: "嵌入和共享数据集 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: adc95cc0-d15a-413d-bc5a-302eab37a069
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb2ff6fdeb8f4d05866c09e87cd899a5dd2bb7ad
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="embedded-and-shared-datasets-report-builder-and-ssrs"></a>嵌入数据集和共享数据集（报表生成器和 SSRS）
  在报表中，数据集表示通过对外部数据源运行查询而返回的报表数据。 数据集依赖于包含有关外部数据源的信息的数据连接。 数据本身并不包含在报表定义中。 数据集包含查询命令、字段集合、参数、筛选器以及数据选项（包括区分大小写和排序规则）。 有两种类型的数据集：  
  
-   **共享数据集。** 共享数据集发布在报表服务器上，可由多个报表使用。 共享数据集必须基于共享数据源。 可以通过创建缓存刷新计划来对共享数据集进行缓存和计划。  
  
-   **嵌入数据集。** 嵌入数据集在单个报表中定义和使用。  
  
 这两种数据源的区别在于其创建、存储和管理的方式不同。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="shared-datasets"></a>共享数据集  
 使用共享数据集可以提供可由多个报表使用的查询。 共享数据集存储在报表服务器上，并与报表或共享数据源分开管理。 例如，报表服务器管理员可能会更新查询，以便利用改进的索引或其他查询性能优化。  
  
 建议您尽量使用共享数据集。 您可以优化查询或缓存查询结果，以提高报表性能。 共享数据集使数据访问更易于管理，并有助于提高报表和报表所访问数据集的访问安全性和性能。  
  
 在报表设计器中，您可以将共享数据集作为报表项目的一部分创建，并且控制是否将这些共享数据集部署到报表服务器。 您不能通过浏览报表服务器来选择某个共享数据集以添加到您的报表中。  
  
 在报表生成器中，您可以执行以下操作：  
  
1.  若要创建共享数据集，请使用共享数据集设计视图。 您可以将其保存到报表服务器或 SharePoint 站点上，以便与其他报表共享。 此外，您还可以通过浏览报表服务器来编辑现有的共享数据集。 在此视图中，您可以生成查询和设置所有数据集选项。 有关详细信息，请参阅[共享数据集设计视图 &#40;报表生成器 &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md).  
  
2.  若要在报表中添加共享数据集，请在“报表设计”视图中打开报表生成器。 从向导或“报表数据”窗格中，浏览到报表服务器，然后选择要添加到报表的共享数据集。 在此视图中，您除了可以添加字段外，不能更改查询。 您可以覆盖其他数据选项并添加筛选器， 但不能删除筛选器。  
  
3.  下表将可为报表服务器上共享数据集的定义配置的属性与可为报表定义中共享数据集的实例配置的属性进行了比较。  
  
    |属性|有关定义的配置说明|有关实例的配置说明|  
    |--------------|--------------------------------------------|------------------------------------------|  
    |查询文本|配置查询，包括将查询定义为表达式。|无法更改查询。|  
    |查询参数|不能引用报表参数<br /><br /> 包含默认值<br /><br /> 包含只读标志|配置定义中未标记为只读的参数|  
    |筛选器|定义筛选器|无法查看或更改作为定义的一部分的数据集筛选器<br /><br /> 可以创建其他筛选器|  
    |数据源|必须为共享数据源|无法更改数据源|  
    |字段|来自查询命令的字段<br /><br /> 计算字段不是数据集定义的一部分|查看字段，但无法对其进行更改<br /><br /> 字段集合是静态的，它基于您向报表中添加共享数据集时所使用的查询。 若要进行更新，请单击 **“数据集属性”** 对话框中的 **“刷新字段”** 。 实际的字段集合可以是定义中当前查询返回的任何集合。<br /><br /> 添加计算字段|  
    |数据集|数据选项，如区分大小写|覆盖实例中的数据选项|  
  
## <a name="embedded-datasets"></a>嵌入的数据集  
 当您希望从外部数据源获取将只在一个报表中使用的数据时，使用嵌入数据集。 当您希望创建没有其他依赖项且不需要用于多个报表的查询时，嵌入数据集非常有用。  
  
 若要创建或编辑嵌入数据集，请使用“报表数据”窗格。 在创建数据集后，您可以在 **“数据集属性”** 对话框中配置属性。  
  
## <a name="see-also"></a>另请参阅  
 [嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)   
 [创建共享数据集或嵌入数据集 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [数据集字段集合 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [数据连接、 数据源和报表生成器中的连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  

