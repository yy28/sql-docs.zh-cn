---
title: 属性数据转换对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.dimensionstoragesettings.f1
helpviewer_keywords:
- Attribute Data Translation dialog box
ms.assetid: bed286de-1e9b-49de-b09e-3cd076aba152
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2304f664178ab1f5d3718cccdcb4b1775a72948e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063064"
---
# <a name="attribute-data-translation-dialog-box-analysis-services---multidimensional-data"></a>“翻译属性数据”对话框（Analysis Services - 多维数据）
  可以使用 **“翻译属性数据”** 对话框设置包含翻译标题数据的列，以及与翻译数据一起使用的排序规则和排序顺序。 通过执行以下操作可以显示 **“翻译属性数据”** 对话框：  
  
-   在 **维度设计器** 的 **“翻译”** 选项卡上，在 **“工具栏”** 窗格中单击 **“新建标题列”** 或 **“编辑标题列”**。  
  
-   在**维度设计器**的“翻译”选项卡上，右键单击“翻译详细信息”窗格，再选择“新建标题列”或“编辑标题列”。  
  
## <a name="options"></a>选项  
 **Attribute**  
 显示所选属性。  
  
 **语言**  
 显示所选语言。  
  
 **已翻译的标题**  
 为所选属性设置当前已翻译的标题。  
  
 **翻译列**  
 设置存储翻译标题数据的列。 只能选择一列。 将显示主维度表引用的所有相关表。  
  
 **排序规则指示符**  
 为所选属性设置排序规则指示符。 默认情况下，选择当前的 Windows 排序规则。 单击下箭头可以从可用的排序规则中进行选择。  
  
 **二进制**  
 选择此选项可根据为每个字符定义的位模式对数据进行排序和比较。 二进制排序顺序区分大小写，即先小写字母后大写字母，并区分重音。 这是最快的排序顺序。  
  
 如果未选择此选项，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将遵循字典中定义的相关语言或字母表的排序和比较规则。  
  
> [!NOTE]  
>  如果选择此选项，将会禁用“区分大小写”、“区分重音”、“区分假名”和“区分全半角”选项。  
  
 **区分大小写**  
 选择此选项可以根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分大小写字母。  
  
 如果不选择此选项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将认为大小写字母是等价的。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不会定义是否排序或字母与大写字母**区分大小写**未选中。  
  
 **区分重音**  
 选择此选项可以根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分重音和非重音字符。 例如，“a”和“á”将被视为不同的字符。  
  
 如果不选择此选项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将认为重音与相应的非重音字母是等价的。  
  
 **区分假名**  
 选择此选项根据为相关的语言或字母表提供的字典规则的数据进行排序和比较并区分两种类型的日语假名字符：平假名和片假名。  
  
 如果不选择此选项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将认为平假名和片假名字符是等价的。  
  
 **区分全半角**  
 选择此选项可以根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分以单字节字符（半角）和双字节字符（全角）表示的相同字符。  
  
 如果不选择此选项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将认为相同字符的单字节表示法和双字节表示法是等价的。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [翻译详细信息&#40;翻译选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](translation-details-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
