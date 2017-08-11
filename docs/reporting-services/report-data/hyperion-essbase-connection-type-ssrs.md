---
title: "Hyperion Essbase 连接类型 (SSRS) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1002bb2ff985a9ee5c2eeaade2377789c136f248
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase 连接类型 (SSRS)
  若要在报表中包含来自 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部数据源的数据，您必须拥有一个基于 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]类型的报表数据源的数据集。 此内置数据源类型基于 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]的数据扩展插件，让你可以从 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 外部数据源检索多维数据。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 下面的连接字符串示例指定使用端口 13080 的服务器上的 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据源以及使用 SOAP 的 Internet 上的 XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA)，并连接到示例目录：  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 有关连接字符串示例的详细信息，请参阅 [报表生成器中的数据连接、数据源和连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅[数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)或[在报表生成器中指定凭据](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查询  
 可以通过下列方式指定查询：  
  
-   以交互方式生成查询。 在设计模式或查询模式下使用图形查询设计器，可浏览外部数据源中的元数据和生成采用多维表达式 (MDX) 语法的查询。  
  
    -   **设计视图** 将维度、成员、成员属性、度量值和 KPI 从元数据浏览器拖至 **“数据”** 窗格，以生成 MDX 查询。 将计算成员从“计算成员”窗格拖至“数据”窗格，以定义附加数据集字段。  
  
    -   **查询视图** 将维度、成员、成员属性、度量值和 KPI 从元数据浏览器拖至“查询”窗格，以生成 MDX 查询。 在“查询”窗格中可以直接编辑 MDX 文本。 将计算成员从“计算成员”窗格拖至“查询”窗格，以定义附加数据集字段。  
  
     有关详细信息，请参阅[Hyperion Essbase 查询设计器用户界面（报表生成器）](http://msdn.microsoft.com/library/d89a6773-dbe5-48e5-bda9-db0e67100696)。  
  
-   从报表导入现有 MDX 查询。 使用 **“导入”** 查询按钮浏览到 .rdl 文件并导入查询。 对于包含基于 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据源的嵌入数据集的报表，可以从中导入查询。 不支持直接从 .mdx 文件导入 MDX 查询。  
  
 在设计时，运行查询以查看结果集。 生成查询后，在“报表数据”窗格中查看从元数据生成的数据集字段集合。 报告运行时，将从外部数据源返回实际数据。  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据处理扩展插件支持扩展数据集字段属性。 这些值可从外部数据源获得，但在“报表数据”窗格中不显示。 有关详细信息，请参阅本主题后面的 [扩展字段属性](#Extended) 。  
  
  
##  <a name="Parameters"></a> 若要包括查询参数，请在查询设计器的筛选区域创建一个筛选器，并将该筛选器标记为参数。 系统将为每个筛选器自动创建一个数据集以提供可用值。 默认情况下，这些数据集不显示在“报表数据”窗格中。 有关详细信息，请参阅[为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS）](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)。  
  
 默认情况下，每个报表参数的数据类型均为 **Text**。 创建报表参数后，您可能需要更改默认值。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)类型的报表数据源的数据集。  
  
  
##  <a name="Extended"></a> 扩展字段属性  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据处理扩展插件支持扩展字段属性。 扩展字段属性是除了通过数据处理扩展插件为数据集字段定义的 **Value** 和 **IsMissing** 之外的其他属性。 扩展属性包括预定义属性和自定义属性。 预定义属性是对多个数据源通用的属性。 自定义属性对于每个数据源都是唯一的。  
  
 扩展字段属性不作为可拖至报表布局的项出现在“报表数据”窗格中。 不过，您可以将该属性的父字段拖至报表中，然后将默认属性由 **Value** 更改为要使用的属性。  
  
 当您将鼠标光标停在查询设计器“元数据”窗格中的某个字段上时，扩展字段属性的名称便会显示在工具提示中。 有关可用于浏览基础数据的查询设计器的详细信息，请参阅 [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)。  
  
> [!NOTE]  
>  仅当扩展字段属性包含在 MDX 表达式中，且数据源在报表运行和为其数据集检索数据的情况下提供扩展字段属性的值时，这些值才存在。 然后，您就可以使用下面一节所述的语法从任意表达式引用这些 **Field** 属性值。 但是，由于这些字段特定于此数据访问接口，而不是报表定义语言的一部分，因此，对这些值所做的更改不会随报表定义一同保存。  
  
  
### <a name="predefined-field-properties"></a>预定义的字段属性  
 通常受多个数据访问接口支持并出现在报表数据集的基础 MDX 查询中的预定义字段属性。 例如，MDX 维度属性 MEMBER_UNIQUE_NAME 映射到预定义报表数据集字段属性 **UniqueName**。 若要在文本框中包含的唯一名称值，使用表达式`=Fields!`  *\<FieldName >*`.UniqueName`。  
  
 下表提供了可以用于 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据源的预定义字段属性的列表。  
  
|**属性**|**类型**|**说明或所需的值**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**对象**|指定字段的数据值。<br /><br /> 对于维度属性，它映射到 MEMBER_CAPTION。 对于度量值，它映射到数据值。|  
|**IsMissing**|**Boolean**|指示是否在结果数据集中找到了该字段。|  
|**FormattedValue**|**字符串**|返回关键数字的格式值。<br /><br /> 映射自 MDX 表达式中的 FORMATTED_VALUE。|  
|**BackgroundColor**|**字符串**|返回数据库中为该字段定义的背景颜色。<br /><br /> 映射自 MDX 表达式中的 BACK_COLOR。|  
|**Color**|**字符串**|返回数据库中为该项定义的前景色。<br /><br /> 映射自 MDX 表达式中的 FORE_COLOR。|  
|**UniqueName**|**字符串**|返回级别的完全限定名称。<br /><br /> 映射自 MDX 表达式中的 MEMBER_UNIQUE_NAME。|  
  
 有关如何在表达式中使用字段和字段属性的详细信息，请参阅[表达式中的内置集合（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
  
### <a name="custom-properties"></a>自定义属性  
 为某个数据访问接口所支持并出现在报表数据集的基础 MDX 查询中的自定义字段属性，但这些属性不作为该数据集的字段出现在报表“数据集”窗格中。 例如， **Long Names** 是为某个维度级别定义的成员属性。 若要在文本框中包含的值，则使用表达式`=Fields!`  *\<FieldName >*`("Long Names")`。 表达式中的字段名区分大小写。  
  
 可以使用以下语法在表达式中引用自定义扩展属性：  
  
-   *Fields!FieldName("PropertyName")*  
  
 下表显示了可用于 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 数据源的自定义字段属性。  
  
|**属性**|**类型**|**说明或所需的值**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**字符串**|针对度量值定义，是可作为 String 类型的 **FormattedValue** 。|  
  
  
##  <a name="Remarks"></a> 注释  
 不是所有的报表传递模式都受到此数据访问接口的支持。 此数据处理扩展插件不支持通过数据驱动订阅传递报表。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ 联机丛书 ](http://go.microsoft.com/fwlink/?linkid=121312) 中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的[使用外部数据源提供订阅方数据（数据驱动订阅）](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
 有关详细信息，请参阅 [Using SQL Server 2005 Reporting Services with Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)（使用具有 Hyperion Essbase 的 SQL Server 2005 Reporting Services）。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明：  
  
 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [将筛选器添加到数据集 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [数据连接、 数据源和报表生成器中的连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供有关数据连接和数据源的信息。  
  
 [报表嵌入数据集和共享数据集 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关数据集查询生成的字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) 部分。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
 [使用 SQL Server 2005 Reporting Services with Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)  
 提供有关使用此数据扩展插件的详细信息。  
  
  
## <a name="see-also"></a>另请参阅  
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [筛选器、 组中，以及对数据进行排序和 #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
