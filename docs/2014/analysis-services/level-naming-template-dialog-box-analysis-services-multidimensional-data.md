---
title: 级别命名模板对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3f7c3bf3d7c1b09d8655443d4de711f851667947
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016260"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>“级别命名模板”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “级别命名模板” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，为维度的父属性构造级别命名模板。 有关级别命名模板的详细信息，请参阅 [NamingTemplate 元素 (ASSL)](scripting/properties/namingtemplate-element-assl.md)。 可以显示**级别命名模板**对话框中单击省略号按钮 (**...**) 上`NamingTemplate`的转换是为中的属性的值**翻译详细信息**在窗格中**翻译**选项卡**维度设计器**.  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**定义级别模板**|显示一个网格，您可以在其中设计父属性中级别的层次结构。 该网格包含以下列：<br /><br /> **级别**： 显示名称中为其指定的级别的序号位置**名称**使用。 若要为级别添加新的命名模板，请在“级别”中包含星号 (\*) 的行上选择“名称”。<br /><br /> **名称**： 包含用于中所示的级别命名模板**级别**。 若要在命名模板中为级别序号位置添加占位符，请添加单个星号 (*)。 若要创建的命名模板的名称的一部分中添加一个星号，添加两个星号 (\*\*)。|  
|**全部清除**|选择此项可以删除 **“定义级别模板”** 中的所有行。|  
|**结果**|显示由对话框生成的级别命名模板。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [翻译&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  