---
title: 分析 Excel (SSAS 表格) 中的表格模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.chooseperspect.f1
ms.assetid: 47fa45fc-60ab-41a1-bde3-5781c8462889
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d838dbf683746b212967f2775c6c943310ce6cb6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204007"
---
# <a name="analyze-a-tabular-model-in-excel-ssas-tabular"></a>在 Excel 中分析表格模型（SSAS 表格）
  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“在 Excel 中分析”功能可以打开 Microsoft Excel、创建到模型工作区数据库的数据源连接以及将数据透视表添加到工作表。 模型对象（表、列、度量值、层次结构和 KPI）作为数据透视表字段列表中的字段包含。  
  
> [!NOTE]  
>  为了使用“在 Excel 中分析”功能，您必须在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]所在的计算机上安装 Microsoft Office 2003 或更高版本。 如果 Office 安装在不同的计算机上，您可以在另一计算机上使用 Excel 并连接到作为数据源的模型工作区数据库。 然后可以将数据透视表手动添加到工作表。 模型对象（表、列、度量值和 KPI）作为数据透视表字段列表中的字段包含。  
  
## <a name="tasks"></a>“任务”  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>使用“在 Excel 中分析”功能分析表格模型项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在 **“选择凭据和透视”** 对话框中，选择以下凭据选项之一以连接到模型工作区数据源：  
  
    -   若要使用当前用户帐户，请选择 **“当前 Windows 用户”**。  
  
    -   若要使用其他用户帐户，请选择 **“其他 Windows 用户”**。  
  
         通常，此用户帐户将是某个角色的成员。 不需要密码。 只能在工作区数据库的 Excel 连接的上下文中使用此帐户。  
  
    -   若要使用安全角色，请选择 **“角色”**，然后在列表框中选择一个或多个角色。  
  
         必须使用角色管理器定义安全角色。 有关详细信息，请参阅[创建和管理角色（SSAS 表格）](roles-ssas-tabular.md)。  
  
3.  若要使用透视，请在 **“透视”** 列表框中选择一个透视。  
  
     必须使用“透视”对话框定义透视（非默认值）。 有关详细信息，请参阅[创建和管理透视表（SSAS 表格）](perspectives-ssas-tabular.md)。  
  
> [!NOTE]  
>  当您在模型设计器中更改模型项目时，Excel 中的数据透视表字段列表不会自动刷新。 若要刷新 Excel 中的数据透视表字段列表，请在 **“选项”** 功能区上单击 **“刷新”**。  
  
## <a name="see-also"></a>请参阅  
 [在 Excel 中分析&#40;SSAS 表格&#41;](analyze-in-excel-ssas-tabular.md)  
  
  
