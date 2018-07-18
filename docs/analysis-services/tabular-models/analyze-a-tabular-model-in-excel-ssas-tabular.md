---
title: 分析在 Excel 中的表格模型 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1db764052a9c3370554a6456dc005612a2e8b95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040651"
---
# <a name="analyze-a-tabular-model-in-excel"></a>分析在 Excel 中的表格模型  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
         必须使用角色管理器定义安全角色。 有关详细信息，请参阅[创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
3.  若要使用透视，请在 **“透视”** 列表框中选择一个透视。  
  
     必须使用“透视”对话框定义透视（非默认值）。 有关详细信息，请参阅[创建和管理透视](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
> [!NOTE]  
>  当您在模型设计器中更改模型项目时，Excel 中的数据透视表字段列表不会自动刷新。 若要刷新 Excel 中的数据透视表字段列表，请在 **“选项”** 功能区上单击 **“刷新”**。  
  
## <a name="see-also"></a>另请参阅  
 [在 Excel 中分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
