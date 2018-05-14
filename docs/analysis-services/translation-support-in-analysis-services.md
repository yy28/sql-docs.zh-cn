---
title: Analysis Services 中的翻译支持 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 882434c2bd0a194a2ecbe21a62d3b22964b30f09
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="translation-support-in-analysis-services"></a>Analysis Services 中的翻译支持
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据模型中，可以嵌入描述文字或说明的多个翻译，从而根据 LCID 提供特定于区域性的字符串。 对于多维模型，你可以为数据库名称、多维数据集对象和数据库维度对象添加翻译。 对于表格模型，你可以为表和列的描述文字和说明添加翻译。  
  
 虽然定义翻译会在模型内创建元数据和已翻译的描述文字，但若要在客户端应用程序中呈现本地化字符串，则必须在对象上设置 **Language** 属性，或在连接字符串上传递 **Culture** 或 **Locale Identifier** 参数（例如，通过设置 `LocaleIdentifier=1036` 返回法语字符串）。  
  
 如果想在不同语言中支持同一对象的多个同时翻译，则应使用 **Locale Identifier** 。 设置 **Language** 属性会发生作用，但它也会影响处理和查询，这可能会产生意外后果。 设置 **Locale Identifier** 是更好的选择，因为它仅用于返回已翻译的字符串。  
  
 一个翻译包括一个区域设置标识符 (LCID)、一个该对象的已翻译标题（例如，维度或属性名称），还可以选择包括以目标语言提供数据值的一个列。 你可以拥有多个翻译，但只能对任意给定连接使用一个翻译。 理论上可以将任意数量的翻译嵌入到模型中，但每个翻译都会增加测试的复杂性，并且所有翻译必须共享同一排序规则，所以设计解决方案时，应考虑到这些自然约束。  
  
> [!TIP]  
>  可以使用客户端应用程序（如 Excel、Management Studio 和 SQL Server Profiler ）来返回已翻译的字符串。 有关详细信息，请参阅 [Globalization Tips and Best Practices &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) 。  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>如何在 Analysis Services 中向模型添加已翻译的元数据  
 有关分步说明，请访问以下链接：  
  
-   [表格模型中的翻译 (Analysis Services)](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [多维模型中的翻译 (Analysis Services)](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 的全球化方案](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [语言和排序规则 & #40;Analysis Services & #41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [设置或更改列排序规则](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [全球化提示和最佳实践和 #40;Analysis Services & #41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
