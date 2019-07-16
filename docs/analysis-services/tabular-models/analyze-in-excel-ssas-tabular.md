---
title: 分析在 Excel 中的 Analysis Services 表格模型 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: abd910573f512e32ee58c6c3afabac17664f4b24
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207762"
---
# <a name="analyze-in-excel"></a>在 Excel 中分析
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在 Excel 功能中，在 SSDT 中，分析帮助表格模型作者在开发期间快速分析模型项目的方法。 使用“在 Excel 中分析”功能可以打开 Microsoft Excel、创建到模型工作区数据库的数据源连接以及自动将数据透视表添加到工作表。 工作区数据库对象（表、列和度量值）作为数据透视表字段列表中的字段包含。 然后可以在有效用户或角色的上下文以及透视中查看对象和数据。  
  
 本文假定你已熟悉 Microsoft Excel、 数据透视表和数据透视图。 若要了解有关使用 Excel 的详细信息，请参阅 Excel 帮助。  
  
##  <a name="bkmk_benefits"></a> 优势  
 借助“在 Excel 中分析”功能，模型创建者使用普通的数据分析应用程序 Microsoft Excel 就可以测试模型项目的效力。 若要使用 Excel 功能中的分析，您必须具有 Microsoft Office 2003 或更高版本安装在 SSDT 所在的计算机上。  
  
 使用“在 Excel 中分析”功能可以打开 Excel 并创建新的 Excel 工作簿 (.xls)。 创建从工作簿到模型工作区数据库的数据连接。 将一个空白数据透视表添加到工作表，并在数据透视表字段列表中填充模型对象元数据。 然后，您可以向数据透视表添加可查看的数据和切片器。  
  
 使用“在 Excel 中分析”功能时，默认情况下当前已登录的用户帐户为有效用户。 此帐户通常为对模型对象或数据没有查看限制的管理员。 但您可以指定其他有效用户名或角色。 这允许您在特定用户或角色的上下文中浏览 Excel 中的模型项目。 以下选项用于指定有效用户：  
  
 **当前 Windows 用户**  
 使用您当前登录的用户帐户。  
  
 **其他 Windows 用户**  
 使用指定的 Windows 用户名而不是当前登录的用户。 使用不同的 Windows 用户不需要密码。 只能在有效用户名的上下文中使用 Excel 查看对象和数据。 在 Excel 中，不能更改模型对象或数据。  
  
 **角色**  
 角色用于定义对对象元数据和数据的用户权限。 通常为特定的 Windows 用户或 Windows 用户组定义角色。 某些角色可以包括 DAX 公式中定义的其他行级筛选器。 使用“在 Excel 中分析”功能时，可以选择要使用的角色（此为可选项）。 对象元数据和数据视图将受为角色定义的权限和筛选器限制。 有关详细信息，请参阅[创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
 除了有效用户或角色之外，您还可以指定透视。 模型创建者使用透视定义模型对象和数据的特殊业务方案视图。 默认情况下，不使用透视。 若要使用与在 Excel 中分析的角度来看，透视必须已定义使用 SSDT 中的透视对话框。 如果指定了透视，数据透视表字段列表将只包含在透视中选择的那些对象。 有关详细信息，请参阅[创建和管理透视](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|**主题**|**说明**|  
|---------------|---------------------|  
|[在 Excel 中分析表格模型](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)|本文介绍如何使用分析在 Excel 功能模型设计器中打开 Excel、 创建到模型工作区数据库的数据源连接并将数据透视表添加到工作表。|  
  
## <a name="see-also"></a>请参阅  
 [分析 Excel 中的表格模型](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [透视](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
