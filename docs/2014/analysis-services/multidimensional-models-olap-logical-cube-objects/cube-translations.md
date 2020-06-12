---
title: 多维数据集翻译 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- cubes [Analysis Services], translations
- OLAP objects [Analysis Services], translations
- translations [Analysis Services], cubes
ms.assetid: 4e4fd6a4-d324-4508-b75a-2a57de9ab8ff
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8cd4347baae8504ef5dd0f13a3adcca634c49ea2
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545267"
---
# <a name="cube-translations"></a>多维数据集翻译
  翻译是将显示的标签和标题从一种语言更改为另一种语言的简单机制。 每个翻译都被定义为一对值：带已翻译文本的字符串和带语言 ID 的数字。 翻译可用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的所有对象。 还可以翻译维度的属性值。 客户端应用程序不但要负责查找用户定义的语言设置，还要将所有标题和标签都切换为以该语言显示。 根据您的需要，一个对象可有多种翻译。  
  
 一个简单的 <xref:Microsoft.AnalysisServices.Translation> 对象由语言 ID 号和翻译后的标题组成。 语言 ID 号是带语言 ID 的 `Integer`。 翻译后的标题是已翻译的文本。  
  
 在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，多维数据集转换是多维数据集对象（如标题或显示文件夹）的名称的特定于语言的表示形式。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还支持维度和成员名称的翻译。  
  
 翻译为可支持多种语言的客户端应用程序提供了服务器支持。 通常，来自不同国家/地区的用户会查看多维数据集数据。 将多维数据集的各种元素翻译为其他语言很有用，因为这样这些用户才能查看并了解多维数据集的元数据。 例如，法国的业务用户可以通过采用了法语区域设置的工作站来访问多维数据集，查看以法语显示的对象属性值。 同样，德国的业务用户可以通过采用了德语区域设置的工作站来访问相同的多维数据集，查看以德语显示的对象属性值。  
  
 客户端计算机的排序规则和语言信息以区域设置标识符 (LCID) 的形式进行存储。 客户端通过连接将 LCID 传递给 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 然后，该实例使用 LCID 来确定在向每个业务用户提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象的元数据时所用的翻译集。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象未包含指定的翻译，则使用默认语言将内容返回给客户端。  
  
## <a name="see-also"></a>另请参阅  
 [维度翻译](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [翻译 &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [全球化提示和最佳实践 (Analysis Services)](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
