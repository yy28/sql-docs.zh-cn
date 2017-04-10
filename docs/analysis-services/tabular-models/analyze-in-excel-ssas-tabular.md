---
title: "在 Excel 中分析（SSAS 表格） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# 在 Excel 中分析（SSAS 表格）
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“在 Excel 中分析”功能为表格模型创建者提供在开发期间快速分析模型项目的方式。 使用“在 Excel 中分析”功能可以打开 Microsoft Excel、创建到模型工作区数据库的数据源连接以及自动将数据透视表添加到工作表。 工作区数据库对象（表、列和度量值）作为数据透视表字段列表中的字段包含。 然后可以在有效用户或角色的上下文以及透视中查看对象和数据。  
  
 本主题假定您已经熟悉如何使用 Microsoft Excel、数据透视表和数据透视图。 若要了解有关使用 Excel 的详细信息，请参阅 Excel 帮助。  
  
 本主题的内容：  
  
-   [优势](#bkmk_benefits)  
  
-   [相关任务](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> 优势  
 借助“在 Excel 中分析”功能，模型创建者使用普通的数据分析应用程序 Microsoft Excel 就可以测试模型项目的效力。 为了使用“在 Excel 中分析”功能，您必须在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]所在的计算机上安装 Microsoft Office 2003 或更高版本。  
  
> [!NOTE]  
>  如果 Office 与 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]安装在不同的计算机上，您可以在另一计算机上使用 Excel 以连接到作为数据源的工作区数据库。 然后可以将数据透视表手动添加到工作表。  
  
 使用“在 Excel 中分析”功能可以打开 Excel 并创建新的 Excel 工作簿 (.xls)。 创建从工作簿到模型工作区数据库的数据连接。 将一个空白数据透视表添加到工作表，并在数据透视表字段列表中填充模型对象元数据。 然后，您可以向数据透视表添加可查看的数据和切片器。  
  
 使用“在 Excel 中分析”功能时，默认情况下当前已登录的用户帐户为有效用户。 此帐户通常为对模型对象或数据没有查看限制的管理员。 但您可以指定其他有效用户名或角色。 这允许您在特定用户或角色的上下文中浏览 Excel 中的模型项目。 以下选项用于指定有效用户：  
  
 **当前 Windows 用户**  
 使用您当前登录的用户帐户。  
  
 **其他 Windows 用户**  
 使用指定的 Windows 用户名而不是当前登录的用户。 使用不同的 Windows 用户不需要密码。 只能在有效用户名的上下文中使用 Excel 查看对象和数据。 在 Excel 中，不能更改模型对象或数据。  
  
 **角色**  
 角色用于定义对对象元数据和数据的用户权限。 通常为特定的 Windows 用户或 Windows 用户组定义角色。 某些角色可以包括 DAX 公式中定义的其他行级筛选器。 使用“在 Excel 中分析”功能时，可以选择要使用的角色（此为可选项）。 对象元数据和数据视图将受为角色定义的权限和筛选器限制。 有关详细信息，请参阅[创建和管理角色（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
 除了有效用户或角色之外，您还可以指定透视。 模型创建者使用透视定义模型对象和数据的特殊业务方案视图。 默认情况下，不使用透视。 为了将透视与“在 Excel 中分析”一起使用，必须已经使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的“透视”对话框定义了透视。 如果指定了透视，数据透视表字段列表将只包含在透视中选择的那些对象。 有关详细信息，请参阅[创建和管理透视表（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> 相关任务  
  
|**主题**|**Description**|  
|---------------|---------------------|  
|[在 Excel 中分析表格模型（SSAS 表格）](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)|本主题说明如何使用模型设计器中的“在 Excel 中分析”功能打开 Excel、创建到模型工作区数据库的数据源连接以及将数据透视表添加到工作表。|  
  
## 另请参阅  
 [在 Excel 中分析表格模型（SSAS 表格）](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [角色（SSAS 表格）](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [透视表（SSAS 表格）](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  