---
title: 多维模型中的翻译 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a80c7950ec4079021bbcf03d9ccee6970d68786b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072735"
---
# <a name="translations-in-multidimensional-models"></a>多维模型中的翻译
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的多语言支持是使用翻译实现的。 翻译包含一个语言标识符，以及可以以多种语言显示的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象属性的绑定。 例如，您可以为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库定义一种翻译，从而以指定的语言显示数据库的标题和说明。 有关翻译的详细信息，请参阅[多维数据集翻译](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)。  
  
## <a name="defining-translations"></a>定义翻译  
 可以通过使用要翻译的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 对象的相应设计器，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中定义翻译。 定义翻译时，将创建一个与相应的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象关联的 `Translation` 对象。对于关联的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的属性，被创建的对象具有以指定语言表示的指定的显式文字值。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的以下对象和属性可以有与之关联的翻译：  
  
|对象|属性|Designer|  
|------------|----------------|--------------|  
|数据库|`Caption`, `Description`|[Analysis Services 多维&#41;数据&#41; &#40;的常规 &#40;数据库设计器](../general-database-designer-analysis-services-multidimensional-data.md)|  
|多维数据集|`Caption`, `Description`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|度量值组|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|度量|`Caption`, `DisplayFolder`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|多维数据集维度 (Cube dimension)|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|透视|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|关键绩效指标 (KPI)|`Caption`, `Description`, `DisplayFolder`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|操作|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|命名集|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|“计算成员”|`Caption`|[翻译 &#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|数据库维度 (Database dimension)|`Caption`, `AttributeAllMember`|[&#41; &#40;Analysis Services 多维&#41;数据的翻译 &#40;维度设计器](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|属性|`Caption`、 `CaptionColumn` <sup>1</sup>、 `AttributeHierarchyDisplayFolder`、 `NamingTemplate`、`MembersWithDataCaption`|[&#41; &#40;Analysis Services 多维&#41;数据的翻译 &#40;维度设计器](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|层次结构|`Caption`, `AllMemberName`|[&#41; &#40;Analysis Services 多维&#41;数据的翻译 &#40;维度设计器](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|级别|`Caption`|[&#41; &#40;Analysis Services 多维&#41;数据的翻译 &#40;维度设计器](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup>属性`CaptionColumn`的属性可以绑定到数据源视图中的列，并且可以使用除了为实例指定的 Windows 排序规则以外的其他翻译。  
  
### <a name="defining-attribute-translations"></a>定义属性翻译  
 与数据库维度中的属性关联的翻译在以下方面与其他翻译的处理方式不同：  
  
-   列绑定（而非显式文字值）可与 `CaptionColumn` 属性关联，因此可以翻译该属性成员的成员名称。  
  
-   可以使用为实例指定的排序规则以外的 Windows 排序规则，因此可针对翻译中指定的语言对属性进行相应分类。  
  
 你可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“翻译属性数据”对话框来定义数据库维度中的属性的翻译****。 有关“翻译属性数据”对话框的详细信息，请参阅[“翻译属性数据”对话框（Analysis Services - 多维数据）](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)****。  
  
## <a name="resolving-translations"></a>解析翻译  
 如果客户端应用程序请求了采用指定语言标识符的信息，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例会尝试将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的数据和元数据解析为最接近的可能语言标识符。 如果客户端应用程序未指定默认语言，或指定了非特定区域设置标识符 (0) 或进程默认语言标识符 (1024)，那么， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用实例的默认语言来返回 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的数据和元数据。  
  
 如果客户端应用程序指定的语言标识符不是默认语言标识符，则该实例将通过所有可用对象的所有可用翻译进行迭代。 如果指定的语言标识符与某个翻译的语言标识符匹配，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将返回该翻译。 如果找不到匹配项，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将尝试使用以下方法之一，返回语言标识符最接近指定语言标识符的翻译。  
  
-   对于下列语言标识符，如果尚未定义指定语言标识符的翻译，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将尝试使用替代语言标识符。  
  
    |指定语言标识符|替代语言标识符|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 中文（中华人民共和国香港特别行政区）|1028-中文（台湾）|  
    |5124-中文（中国澳门特别行政区）|1028-中文（台湾）|  
    |1028-中文（台湾）|默认语言|  
    |4100 - 中文（新加坡）|2052 - 中文（中华人民共和国）|  
    |2074 - 克罗地亚语|默认语言|  
    |3098 - 克罗地亚语（西里尔文）|默认语言|  
  
-   对于所有其他指定语言标识符， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将提取指定语言标识符的主要语言，并检索 Windows 指示的语言标识符作为主要语言的最佳匹配项。 如果找不到最佳匹配语言标识符的翻译，或者指定的语言标识符是主要语言的最佳匹配项，则将使用默认语言。  
  
## <a name="deleting-translation-objects"></a>删除 Translation 对象  
 您可以在维度或多维数据集设计器中右键单击一个 translation 对象以便永久删除它。 您不能还原或回收已删除的对象，因此在继续之前请务必查看受影响对象的列表。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services Multidimensional 的全球化方案](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [语言和排序规则 (Analysis Services)](../languages-and-collations-analysis-services.md)  
  
  
