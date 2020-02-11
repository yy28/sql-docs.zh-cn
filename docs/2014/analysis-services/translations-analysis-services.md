---
title: 翻译（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e97c9ba15aab664e9f0c77f9eb84152f75c3e3d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065881"
---
# <a name="translations-analysis-services"></a>翻译 (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]** 仅多维  
  
 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据模型中，可以嵌入一个标题的多个翻译，以基于 LCID 提供特定于区域设置的字符串。 可为数据库名称、多维数据集对象和数据库维度对象添加翻译。  
  
 定义翻译将在模型内创建元数据和已翻译的标题，但若要在客户端应用程序中呈现本地化字符串，必须设置对象上的 `Language` 属性，或传递连接字符串上的 `Locale Identifier` 参数（例如，通过设置 `LocaleIdentifier=1036` 返回法语设置）。 如果想在不同语言中支持同一对象的多个同时翻译，则应使用 `Locale Identifier`。 设置 `Language` 属性会发生作用，但它也会影响处理和查询，这可能会产生意外后果。 设置 `Locale Identifier` 是更好的选择，因为它仅用于返回已翻译的字符串。  
  
 一个翻译包括一个区域设置标识符 (LCID)、一个该对象的已翻译标题（例如，维度或属性名称），还可以选择包括以目标语言提供数据值的一个列。 你可以拥有多个翻译，但只能对任意给定连接使用一个翻译。 理论上可以将任意数量的翻译嵌入到模型中，但每个翻译都会增加测试的复杂性，并且所有翻译必须共享同一排序规则，所以设计解决方案时，应考虑到这些自然约束。  
  
> [!TIP]  
>  可以使用客户端应用程序（如 Excel、Management Studio 和 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] ）来返回已翻译的字符串。 有关详细信息，请参阅 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 。  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>设置模型以支持已翻译的成员  
 在多语言解决方案中使用的数据模型不只需要已翻译的标签（字段名称和说明）。 它还需要提供在各种语言脚本中清晰说明的数据值。 若要实现多语言解决方案，则需要你具有独立的属性，且这些属性要绑定到外部数据库中返回该数据的列。  
  
 Adventure Works 示例数据库（多维以及关系数据仓库）展示了翻译功能。 示例模型包含已翻译的标题和说明。 示例关系数据仓库包含已翻译值的列，这些值提供模型中已本地化的属性成员。  
  
 要查看可用于模型的已翻译数据值：  
  
1.  在设计器中打开 Adventure Works 多维模型。  
  
2.  在解决方案资源管理器中，打开 "数据源视图"，然后双击 "\<艾德作品 DW 版本">。  
  
3.  找到 dimDate、dimProduct、dimProductCategory 或 dimProductSubcateogry。 所有这些维度均包含月份、每周天数、产品名称、类别名称等已翻译成员的属性。  
  
4.  右键单击任一字段并选择“浏览数据” ****。 你将看到每个成员的英语、西班牙语和法语翻译。  
  
 日期、时间和货币的格式不通过翻译实现。 若要根据客户端的区域设置动态提供区域特定的格式，请使用货币换算向导和 `FormatString` 属性。 有关详细信息，请参阅 [货币换算 (Analysis Services)](currency-conversions-analysis-services.md) 和 [FormatString 元素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl)。  
  
 第[9 课：在 Analysis Services 中定义透视和翻译](lesson-9-defining-perspectives-and-translations.md)教程将引导你完成创建和测试翻译的步骤。  
  
## <a name="defining-translations"></a>定义翻译  
 定义翻译将创建一个 `Translation` 对象，作为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库、维度或多维数据集对象的子对象。 使用 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 打开解决方案和定义翻译。  
  
### <a name="add-translations-to-a-cube"></a>向多维数据集添加翻译  
 可将翻译添加到多维数据集、度量值组、度量值、多维数据集维度、透视、KPI、操作、命名集和计算成员。  
  
1.  在解决方案资源管理器中，双击多维数据集名称，以打开多维数据集设计器。  
  
2.  单击 "**翻译**" 选项卡。此页中列出了支持翻译的所有对象。  
  
3.  为每个对象指定目标语言（内部解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
     请记住你无法更改排序规则。 一个多维数据集实质上使用一个排序规则，即使你通过已翻译的标题支持多种语言（有一个多维属性的例外情况，如下讨论）。 如果语言不按照共享的排序规则进行正确排序，则只为了满足排序规则要求就需要创建多维数据集的副本。  
  
4.  生成和部署项目。  
  
5.  使用客户端应用程序（如 Excel）连接到数据库，修改连接字符串以使用区域设置标识符。 有关详细信息，请参阅 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 。  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>向维度和属性添加翻译  
 你可以将翻译添加到数据库维度、属性、层次结构和层次结构内的各级别。  
  
 已使用键盘或复制粘贴操作手动将已翻译的标题添加到模型，但对于维度属性成员，则可以从外部数据库中获取已翻译的值。 尤其是，特性的 `CaptionColumn` 属性可绑定到数据源视图中的某列上。  
  
 你可在属性级别覆盖排序规则设置，例如，你可能想要调整全半角区分，或对特定属性使用二进制排序。 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，排序规则在定义数据绑定的位置公开。 因为你正在将维度属性绑定到 DSV 中的不同源列，所有排序规则设置可用，使你可以指定源列所使用的排序规则。 有关关系数据库中列排序规则的详细信息，请参阅 [Set or Change the Column Collation](../relational-databases/collations/set-or-change-the-column-collation.md) 。  
  
1.  在解决方案资源管理器中，双击维度名称，以打开维度设计器。  
  
2.  单击 "**翻译**" 选项卡。此页中列出了支持翻译的所有维度对象。  
  
     为每个对象指定目标语言（解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
3.  要将属性绑定到提供已翻译值的列：  
  
    1.  仍然是在维度设计器 |“翻译” ****，添加一个新翻译。 选择语言。 页面上将出现新的一列来接受已翻译的值。  
  
    2.  将光标置于与其中一个属性相邻的空单元格中。 该属性不能为密钥，但所有其他属性均可选。 你会看到一个内含一个点的小按钮。 单击该按钮以打开“翻译属性数据对话框” ****。  
  
    3.  为标题输入一个翻译。 这在目标语言中用作数据标签，例如，在 PivotTable 字段列表中用作字段名。  
  
    4.  选择提供属性成员的已翻译值的源列。 只有预先存在于绑定到维度的表或查询中的列可用。 如果该列不存在，则需要修改数据源视图、维度和多维数据集以提取该列。  
  
    5.  选择排序规则和排序顺序（如果适用）。  
  
4.  生成和部署项目。  
  
5.  使用客户端应用程序（如 Excel）连接到数据库，修改连接字符串以使用区域设置标识符。 有关详细信息，请参阅 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) 。  
  
### <a name="add-a-translation-of-the-database-name"></a>添加数据库名称的一个翻译  
 你可以在数据库级别为数据库名称和说明添加翻译。 已翻译的数据库名称可能在指定语言的 LCID 的客户端连接上可见，但这取决于工具。 例如，在 Management Studio 中查看数据库将不会显示已翻译的名称，即使你在连接上指定了区域设置标识符。 Management Studio 用以连接 Analysis Services 的 API 不会读取 `Language` 属性。  
  
1.  在解决方案资源管理器中，右键单击项目名称 |“编辑数据库” **** ，以打开数据库设计器。  
  
2.  在翻译中指定目标语言（解析为 LCID）、已翻译的标题和已翻译的说明。 无论是在 Management Studio 中设置服务器语言，还是在单个属性上添加翻译覆盖，语言列表在整个 Analysis Service 中都是一致的。  
  
3.  在数据库的“属性”页，将 `Language` 设置为你对翻译指定的同一 LCID。 或者，如果默认值不再具有意义，也可以设置 `Collation`。  
  
4.  生成和部署数据库。  
  
## <a name="resolving-translations"></a>解析翻译  
 如果客户端应用程序要求区域设置标识符， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例会尝试将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据解析为最匹配的 LCID。 如果客户端应用程序未指定默认语言，或指定了非特定区域设置标识符 (0) 或进程默认语言标识符 (1024)，那么， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将使用实例的默认语言来返回 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services Multidimensional 的全球化方案](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [语言和排序规则 &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)   
 [设置或更改列排序规则](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [全球化提示和最佳做法 &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)  
  
  
