---
title: 翻译详细信息 （翻译选项卡，维度设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbeaebfc7eab6041bb547f18dacfc01aef3d5117
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179017"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>翻译详细信息（“翻译”选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用维度设计器中的 **“翻译”** 选项卡上的 **“翻译详细信息”** 窗格，定义和管理当前所选维度的翻译。  
  
 **若要显示翻译详细信息窗格**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目，然后打开所需的维度。  
  
2.  单击 **“翻译”** 选项卡。  
  
## <a name="options"></a>选项  
 **默认语言**  
 以默认语言设置维度对象的名称。  
  
 **对象类型**  
 显示将翻译的属性。 只能翻译已指定值的对象和属性。 可以翻译以下属性：  
  
-   维度  
  
     `Caption` 和`AttributeAllMember`属性  
  
-   Attribute  
  
     `Caption``AttributeHierarchyDisplayFolder`，和`NamingTemplate`属性  
  
    > [!NOTE]  
    >  只有父属性才具有 `NamingTemplate` 属性。  
  
-   层次结构  
  
     `Caption` 和`AllMemberName`属性  
  
-   级别  
  
     `Caption` 属性  
  
 **\<语言 >**  
 在所选语言中键入或选择维度对象的属性值。 单击省略号按钮 (**...**) 可打开其他对话框，具体取决于所编辑的属性：  
  
-   `NamingTemplate` 属性  
  
     显示[“级别命名模板”对话框（Analysis Services - 多维数据）](level-naming-template-dialog-box-analysis-services-multidimensional-data.md)。  
  
-   `Caption` 属性 （针对特性）  
  
     显示[“翻译属性数据”对话框（Analysis Services - 多维数据）](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="shortcut-menu"></a>快捷菜单  
 右键单击“翻译详细信息”窗格中的翻译，所显示的快捷菜单中以下选项可用：  
  
 **新建翻译**  
 选择此项将显示 **“选择语言”** 对话框并创建一个新翻译。 该翻译将在 **“翻译详细信息”** 网格中显示为一个新列。  
  
 **删除翻译**  
 选择此项将会删除选定翻译。  
  
> [!NOTE]  
>  只有右键单击一个要删除其中翻译的单元后，才可启用该选项。  
  
 **新建标题列**  
 在“翻译详细信息”网格中修改属性时，选择此项将显示“翻译属性数据”对话框，并可以定义新的标题列。 若要启用此选项，必须在 **“翻译详细信息”** 网格中选择了属性的翻译列中的某个单元。  
  
> [!NOTE]  
>  只有右键单击一个单元删除属性的翻译列后，才可启用该选项。  
  
 **编辑标题列**  
 在“翻译详细信息”网格中修改属性时，选择此项将显示“翻译属性数据”对话框，并可以修改现有标题列。  
  
> [!NOTE]  
>  只有在“翻译详细信息”网格中选择了包含属性标题列的翻译列中的某个单元时，才会启用该选项。  
  
 **删除标题列**  
 选择此项将删除在“翻译详细信息”网格中所选属性的标题列。  
  
> [!NOTE]  
>  只有右键单击翻译列中包含属性标题列的单元时，才可启用该选项。  
  
 **显示所有属性**  
 选择此项将对为所选维度定义的所有属性（包括为属性层次结构所禁用的属性）切换显示。  
  
## <a name="see-also"></a>请参阅  
 [翻译&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
