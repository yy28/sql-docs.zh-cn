---
title: "多维模型 (Analysis Services) 中的翻译 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 97c2f9950f050c1e737eebfd0f684ad8cd1e5850
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>多维模型中的翻译 (Analysis Services)
  可以通过使用要翻译的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 对象的相应设计器，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中定义翻译。 定义翻译时，将创建一个与相应的 **对象关联的** 翻译 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。对于关联的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的属性，被创建的对象具有以指定语言表示的指定的显式文字值。  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>多语言数据模型的元素  
 在多语言解决方案中使用的数据模型不只需要已翻译的标签（字段名称和说明）。 它还需要提供在各种语言脚本中清晰说明的数据值。 若要实现多语言解决方案，则需要你具有独立的属性，且这些属性要绑定到外部数据库中返回该数据的列。  
  
 Adventure Works 示例数据库（多维以及关系数据仓库）演示了 Analysis Services 的翻译功能。 示例模型包含已翻译的标题和说明。 示例关系数据仓库包含已翻译值的列，这些值提供模型中已本地化的属性成员。  
  
 要查看可用于模型的已翻译数据值：  
  
1.  在设计器中打开 Adventure Works 多维模型。  
  
2.  在解决方案资源管理器，打开数据源视图，并双击 Adventure Works DW\<版本 >.dsv。  
  
3.  找到 dimDate、dimProduct、dimProductCategory 或 dimProductSubcateogry。 所有这些维度均包含月份、每周天数、产品名称、类别名称等已翻译成员的属性。  
  
4.  右键单击任一字段并选择“浏览数据” 。 你将看到每个成员的英语、西班牙语和法语翻译。  
  
 日期、时间和货币的格式不通过翻译实现。 若要根据客户端的区域设置动态提供区域特定的格式，请使用货币换算向导和 **FormatString** 属性。 有关详细信息，请参阅 [货币换算 (Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md) 和 [FormatString 元素 (ASSL)](../../analysis-services/scripting/properties/formatstring-element-assl.md)。  
  
 Analysis Services 教程中的[Lesson 9: Defining Perspectives and Translations](../../analysis-services/lesson-9-defining-perspectives-and-translations.md) 将引导你完成创建和测试翻译的所有步骤。  
  
## <a name="defining-translations"></a>定义翻译  
  
### <a name="add-translations-to-a-cube"></a>向多维数据集添加翻译  
 可将翻译添加到多维数据集、度量值组、度量值、多维数据集维度、透视、KPI、操作、命名集和计算成员。  
  
1.  在解决方案资源管理器中，双击多维数据集名称，以打开多维数据集设计器。  
  
2.  单击 **“翻译”** 选项卡。此页中列出了支持翻译的所有对象。  
  
3.  为每个对象指定目标语言（内部解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
     请记住你无法更改排序规则。 一个多维数据集实质上使用一个排序规则，即使你通过已翻译的标题支持多种语言（有一个多维属性的例外情况，如下讨论）。 如果语言不按照共享的排序规则进行正确排序，则只为了满足排序规则要求就需要创建多维数据集的副本。  
  
4.  生成和部署项目。  
  
5.  使用客户端应用程序（如 Excel）连接到数据库，修改连接字符串以使用区域设置标识符。 有关详细信息，请参阅[全球化提示和最佳实践 (Analysis Services)](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)。  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>向维度和属性添加翻译  
 你可以将翻译添加到数据库维度、属性、层次结构和层次结构内的各级别。  
  
 已使用键盘或复制粘贴操作手动将已翻译的标题添加到模型，但对于维度属性成员，则可以从外部数据库中获取已翻译的值。 尤其是，特性的 **CaptionColumn** 属性可绑定到数据源视图中的某列上。  
  
 你可在属性级别覆盖排序规则设置，例如，你可能想要调整全半角区分，或对特定属性使用二进制排序。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，排序规则在定义数据绑定的位置公开。 因为你正在将维度属性绑定到 DSV 中的不同源列，所有排序规则设置可用，使你可以指定源列所使用的排序规则。 有关关系数据库中列排序规则的详细信息，请参阅 [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) 。  
  
1.  在解决方案资源管理器中，双击维度名称，以打开维度设计器。  
  
2.  单击 **“翻译”** 选项卡。此页中列出了支持翻译的所有维度对象。  
  
     为每个对象指定目标语言（解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
3.  要将属性绑定到提供已翻译值的列：  
  
    1.  仍然是在维度设计器 |“翻译” ，添加一个新翻译。 选择语言。 页面上将出现新的一列来接受已翻译的值。  
  
    2.  将光标置于与其中一个属性相邻的空单元格中。 该属性不能为密钥，但所有其他属性均可选。 你会看到一个内含一个点的小按钮。 单击该按钮以打开“翻译属性数据对话框” 。  
  
    3.  为标题输入一个翻译。 这在目标语言中用作数据标签，例如，在 PivotTable 字段列表中用作字段名。  
  
    4.  选择提供属性成员的已翻译值的源列。 只有预先存在于绑定到维度的表或查询中的列可用。 如果该列不存在，则需要修改数据源视图、维度和多维数据集以提取该列。  
  
    5.  选择排序规则和排序顺序（如果适用）。  
  
4.  生成和部署项目。  
  
5.  使用客户端应用程序（如 Excel）连接到数据库，修改连接字符串以使用区域设置标识符。 有关详细信息，请参阅[全球化提示和最佳实践 (Analysis Services)](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)。  
  
### <a name="add-a-translation-of-the-database-name"></a>添加数据库名称的一个翻译  
 你可以在数据库级别为数据库名称和说明添加翻译。 已翻译的数据库名称可能在指定语言的 LCID 的客户端连接上可见，但这取决于工具。 例如，在 Management Studio 中查看数据库将不会显示已翻译的名称，即使你在连接上指定了区域设置标识符。 Management Studio 用以连接 Analysis Services 的 API 不会读取 **Language** 属性。  
  
1.  在解决方案资源管理器中，右键单击项目名称 |“编辑数据库”  ，以打开数据库设计器。  
  
2.  在翻译中指定目标语言（解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
3.  在数据库的“属性”页，将 **Language** 设置为你对翻译指定的同一 LCID。 或者，如果默认值不再具有意义，也可以设置 **Collation** 。  
  
4.  生成和部署数据库。  
  
## <a name="deleting-translation-objects"></a>删除 Translation 对象  
 您可以在维度或多维数据集设计器中右键单击一个 translation 对象以便永久删除它。 您不能还原或回收已删除的对象，因此在继续之前请务必查看受影响对象的列表。  
  
## <a name="resolving-translations"></a>解析翻译  
 如果客户端应用程序请求了采用指定语言标识符的信息，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例会尝试将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的数据和元数据解析为最接近的可能语言标识符。 如果客户端应用程序未指定默认语言，或指定了非特定区域设置标识符 (0) 或进程默认语言标识符 (1024)，那么， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用实例的默认语言来返回 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的数据和元数据。  
  
 如果客户端应用程序指定的语言标识符不是默认语言标识符，则该实例将通过所有可用对象的所有可用翻译进行迭代。 如果指定的语言标识符与某个翻译的语言标识符匹配，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将返回该翻译。 如果找不到匹配项，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将尝试使用以下方法之一，返回语言标识符最接近指定语言标识符的翻译。  
  
-   对于下列语言标识符，如果尚未定义指定语言标识符的翻译，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将尝试使用替代语言标识符。  
  
    |指定语言标识符|替代语言标识符|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 中文（中华人民共和国香港特别行政区）|1028 - 中文（中国台湾）|  
    |5124 - 中文（中国澳门特别行政区）|1028 - 中文（中国台湾）|  
    |1028 - 中文（中国台湾）|默认语言|  
    |4100 - 中文（新加坡）|2052 - 中文（中华人民共和国）|  
    |2074 - 克罗地亚语|默认语言|  
    |3098 - 克罗地亚语（西里尔文）|默认语言|  
  
-   对于所有其他指定语言标识符， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将提取指定语言标识符的主要语言，并检索 Windows 指示的语言标识符作为主要语言的最佳匹配项。 如果找不到最佳匹配语言标识符的翻译，或者指定的语言标识符是主要语言的最佳匹配项，则将使用默认语言。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 的全球化方案](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [语言和排序规则 &#40;Analysis Services &#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
