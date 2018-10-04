---
title: 维度翻译 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99c7bb8501d386aeac0496e975a5df6d6353a25d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131077"
---
# <a name="dimension-translations"></a>维度翻译
  翻译是将显示的标签和标题从一种语言更改为另一种语言的简单机制。 每个翻译都被定义为一对值：带已翻译文本的字符串和带语言 ID 的数字。 翻译可用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的所有对象。 还可以翻译维度的属性值。 客户端应用程序不但要负责查找用户定义的语言设置，还要将所有标题和标签都切换为以该语言显示。 根据您的需要，一个对象可有多种翻译。  
  
 一个简单的 <xref:Microsoft.AnalysisServices.Translation> 对象由语言 ID 号和翻译后的标题组成。 语言 ID 号是带语言 ID 的 `Integer`。 翻译后的标题是已翻译的文本。  
  
 在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，维度翻译是维度的名称的名称的特定于语言的表示形式[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象或其成员，如标题、 成员或层次结构级别之一。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 此外支持多维数据集对象的翻译。  
  
 翻译为可支持多种语言的客户端应用程序提供了服务器支持。 通常，来自不同国家/地区的用户都会查看多维数据集及其维度。 将多维数据集及其维度的各种元素翻译为其他语言很有用，因为这样这些用户才能查看并了解多维数据集。 例如，法国的业务用户可以从使用法语区域设置，工作站访问多维数据集并查看以法语的对象属性值。 但是，德国的业务用户如果通过采用了德语区域设置的工作站来访问相同的多维数据集，则会看到以德语显示的同一对象属性值。  
  
 客户端计算机的排序规则和语言信息以区域设置标识符 (LCID) 的形式进行存储。 客户端通过连接将 LCID 传递给 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 实例使用 LCID 来确定在为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象提供元数据时所用的翻译集。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象未包含指定的翻译，则使用默认语言将内容返回给客户端。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集翻译](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [翻译&#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [全球化提示和最佳实践&#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
