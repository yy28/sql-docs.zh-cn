---
title: 标识符 (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], identifiers
- delimited identifiers [DMX]
- DMX [Analysis Services], identifiers
- identifiers [DMX]
- regular identifiers [DMX]
- names [DMX]
ms.assetid: fbb487a7-1b89-482a-977e-f079379d44fc
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c5726b7550b0c7a9b1dab63344631502b2fa06b7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="identifiers-dmx"></a>标识符 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  中的所有对象[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]必须具有的标识符。 对象的名称便是它的标识符。 服务器、 数据库和数据库对象，如数据源、 数据源视图、 多维数据集、 维度、 挖掘模型等有标识符。  
  
 数据挖掘扩展插件 (DMX) 中有两类标识符：  
  
-   [常规标识符](#RegularIdentifiers)  
  
-   [分隔的标识符](#DelimitedIdentifiers)  
  
 定义对象时会创建一个对象标识符。 然后，可使用该标识符来引用对象。 标识符包含的字符数必须小于或等于 100。  
  
##  <a name="RegularIdentifiers"></a>常规标识符  
 DMX 中的常规标识符符合 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在标识符格式方面的规则。 DMX 中的常规标识符不需要分隔符。 以下是使用常规、 非分隔标识符的 DMX 语句的示例：  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>常规标识符规则  
 下面是有关常规标识符格式的规则：  
  
1.  常规标识符的第一个字符必须是下列字符之一：  
  
    -   如 Unicode 标准 2.0 定义的字母。 包括从 a 到 z 和从 A 到 Z 的拉丁字符以及其他语言的字母字符。  
  
    -   下划线 (_)。  
  
2.  后续字符可以是：  
  
    -   在 Unicode 标准 2.0 定义的字母。  
  
    -   基本拉丁字符或其他国家/地区字符中的十进制数字。  
  
    -   下划线 (_)。  
  
3.  标识符必须不能是 DMX 保留字。 DMX 中的保留字不区分大小写。 有关详细信息，请参阅[保留关键字 &#40; DMX &#41;](../dmx/reserved-keywords-dmx.md)。  
  
4.  标识符不能包含嵌入的空格或特殊字符。  
  
 在 DMX 语句中使用不符合上述规则的标识符时，必须使用方括号分隔这些标识符。  
  
##  <a name="DelimitedIdentifiers"></a>分隔的标识符  
 分隔标识符括在方括号 ([ ]) 中。  下面是一个 DMX 语句示例，其中的分隔标识符符合上述规则。  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 不符合常规标识符格式规则的标识符必须使用分隔符。 下面是一个 DMX 语句示例，其中的分隔标识符包含一个空格：  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 请在下列情况下使用分隔标识符：  
  
-   使用保留关键字作为对象名或对象名的一部分时。  
  
     建议您不要将保留关键字用作对象名。 从早期版本的升级的数据库[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可能包含的早期版本中包含的单词时未保留的标识符[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]但保留的字[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 只有在使用分隔标识符引用此类对象后，才能更改对象的名称。  
  
-   使用未被列为限定标识符的字符时。  
  
     在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，可以在分隔标识符中使用当前代码页中的任何字符。但是，在对象名称中不加选择地使用特殊字符将使 DMX 语句难以阅读和维护。  
  
### <a name="rules-for-delimited-identifiers"></a>分隔标识符规则  
 以下是分隔标识符的格式规则：  
  
1.  分隔标识符可以包含与常规标识符相同的字符数（1 到 100 个，不包括分隔符本身）。  
  
2.  标识符的主体可以包含当前代码页内所用字符（包括分隔符本身）的任意组合。 如果标识符的主体本身包含分隔符，则需进行特殊处理：  
  
    -   如果标识符的主体包含左方括号 ([)，则无需进行额外处理。  
  
    -   如果标识符的主体包含一个右方括号 (])，则必须指定两个右方括号 (]])，以在代码页中对其进行表示。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>分成多个部分的标识符  
 使用限定对象名称时，可能要分隔组成对象名的多个标识符。 必须单独分隔每个标识符。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
