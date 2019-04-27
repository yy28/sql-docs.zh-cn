---
title: 警告 （数据库设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d83620c0c6463bd6e752f65a97b2fb14e1d1c03f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756012"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>警告（数据库设计器）（Analysis Services - 多维数据）
  使用“警告”选项卡可以全局查看和解除规则，并可以查看和重新启用已解除的警告的特定实例。 **警告**选项卡显示两个网格：**设计警告规则**并**已解除的警告**。  
  
 **若要显示警告选项卡**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目。  
  
2.  在**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目，单击“编辑数据库”，然后单击“警告”选项卡。  
  
## <a name="design-warning-rules-grid"></a>“设计警告规则”网格  
 **“设计警告规则”** 网格显示所有设计警告规则。 此网格还控制对数据库所启用的规则。 若要启用或禁用某个警告规则，请选中或清除其复选框。  
  
 **“设计警告规则”** 网格包含以下列：  
  
 **说明**  
 显示规则的名称。 规则会按类别分组。  
  
 **重要性**  
 显示分配给规则的重要性。  
  
 **注释**  
 （可选）允许用户键入注释，对解除警告的原因进行解释。  
  
## <a name="dismissed-warnings-grid"></a>“解除的警告”网格  
 **“解除的警告”** 网格显示所有已从 **“错误列表”** 解除的特定警告。 若要重新启用某个警告，请在网格中选择该警告，然后单击“重新启用”。  
  
 **“解除的警告”** 网格包含以下内容：  
  
 **Object**  
 显示代表对象类型和对象名称的图标。  
  
 **类型**  
 显示对象类型。  
  
 **说明**  
 显示规则的名称。  
  
 **重要性**  
 显示分配给规则的重要性。  
  
 **注释**  
 显示解除该警告时输入的注释。 可在此添加或修改注释。  
  
 **Re-enable**  
 重新启用选定的警告。  
  
> [!NOTE]  
>  如果对象包含警告，但是该对象处于无效状态或已从项目中手动删除，则列表中该警告的旁边会出现错误图标。 若要解除该警告，请选择它，然后单击“重新启用”。  
  
## <a name="see-also"></a>请参阅  
 [关闭警告对话框&#40;Analysis Services-多维数据&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [常规&#40;数据库设计器&#41; &#40;Analysis Services-多维数据&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
