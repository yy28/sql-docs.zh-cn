---
title: 级别命名模板对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4b0a858c3e87aa657f02d106f6e6db453ee0cb0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088327"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>“级别命名模板”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “级别命名模板” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，为维度的父属性构造级别命名模板。 有关级别命名模板的详细信息，请参阅 [NamingTemplate 元素 (ASSL)](scripting/properties/namingtemplate-element-assl.md)。 可以显示**级别命名模板**对话框中，通过单击省略号按钮 (**...**) 上`NamingTemplate`转换中的属性的值**翻译详细信息**窗格**翻译**选项卡**维度设计器**.  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**定义级别模板**|显示一个网格，您可以在其中设计父属性中级别的层次结构。 该网格包含以下列：<br /><br /> **级别**： 显示名称中指定级别的序号位置**名称**使用。 若要为级别添加新的命名模板，请在“级别”中包含星号 (\*) 的行上选择“名称”。<br /><br /> **名称**： 包含用于在所指示级别的命名模板**级别**。 若要在命名模板中为级别序号位置添加占位符，请添加单个星号 (*)。 若要添加星号作为命名模板创建的名称的一部分，请添加两个星号 (\*\*)。|  
|**全部清除**|选择此项可以删除 **“定义级别模板”** 中的所有行。|  
|**结果**|显示由对话框生成的级别命名模板。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [翻译&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
