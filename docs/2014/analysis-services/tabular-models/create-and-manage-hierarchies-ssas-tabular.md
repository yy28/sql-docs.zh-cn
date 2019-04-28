---
title: 创建和管理层次结构 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 8dd30cd0-a831-4d25-b577-648d7f3c7fa6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bda916232a3d1b0c46a4278def28ec3759e346d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62795376"
---
# <a name="create-and-manage-hierarchies-ssas-tabular"></a>创建和管理层次结构（SSAS 表格）
  可以在模型设计器的关系图视图中创建和管理层次结构。 若要在关系图视图中查看模型设计器，请在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中单击 **“模型”** 菜单，然后指向 **“模型视图”**，再单击 **“关系图视图”**。  
  
 本主题包括以下任务：  
  
-   [创建层次结构](#bkmk_create)  
  
-   [编辑层次结构](#bkmk_edit)  
  
-   [删除层次结构](#bkmk_delete)  
  
##  <a name="bkmk_create"></a> 创建层次结构  
 您可以通过使用列和表上下文菜单，创建层次结构。 创建层次结构时，一个新的父级别将与您作为子级别选择的列一起出现。  
  
#### <a name="to-create-a-hierarchy-from-the-context-menu"></a>从上下文菜单创建层次结构  
  
1.  在模型设计器（关系图视图）的表窗口中，右键单击某一列，然后单击“创建层次结构”。  
  
     若要选择多列，请单击每一列，右键单击以便打开上下文菜单，然后单击“创建层次结构”。  
  
     一个父层次结构级别将在表窗口的底部创建，并且所选列将作为子级别复制到该层次结构的下方。  
  
2.  键入层次结构的名称。  
  
 可以将其他列拖到层次结构的父级别，这将复制这些列。 将子级别放到层次结构中您希望其出现的位置。  
  
> [!NOTE]  
>  如果您多选度量值以及一个或多个列，或者如果您从多个表中选择列，则在上下文菜单中将禁用“创建层次结构”命令。  
  
##  <a name="bkmk_edit"></a> 编辑层次结构  
 您可以重命名层次结构，重命名子级别，更改子级别的顺序，添加附加列作为子级别，从层次结构中删除子级别，显示子级别的源名称（列名），以及在子级别与层次结构父级别同名的情况下隐藏子级别。  
  
#### <a name="to-change-the-name-of-a-hierarchy-or-child-level"></a>更改层次结构或子级别的名称  
  
1.  右键单击层次结构父级别或子级别，然后单击“重命名”。  
  
2.  键入新名称或者编辑现有名称。  
  
#### <a name="to-change-the-order-of-a-child-level-in-a-hierarchy"></a>更改层次结构中子级别的顺序  
  
-   单击并将子级别拖入到层次结构上的新位置中。  
  
-   或者，右键单击层次结构的某一子级别，然后单击“上移”以便在列表中上移该级别，或单击“下移”以便在列表中下移该级别。  
  
-   或者，右键单击某一子级别以便选择它，然后按下 Alt + 向上箭头以便上移该级别，或按下 Alt + 向上箭头以便在列表中下移该级别。  
  
#### <a name="to-add-another-child-level-to-a-hierarchy"></a>向层次结构添加其他子级别  
  
-   单击并将列拖到父级别或者层次结构的特定位置。 该列将作为层次结构中的子级别复制。  
  
-   或者，右键单击某一列，指向“添加到层次结构”，然后单击该层次结构。  
  
> [!NOTE]  
>  您可以将隐藏的列（从报表中隐藏的列）作为子级别添加到层次结构。 该子级别并不隐藏。  
  
#### <a name="to-remove-a-child-level-from-a-hierarchy"></a>从层次结构中删除子级别  
  
-   右键单击子级别，然后单击“从层次结构中删除”。  
  
-   或者，单击某一子级别，然后按下 **Delete**键。  
  
> [!NOTE]  
>  如果您重命名某一层次结构子级别，则该子级别将不再与从其复制的列共享相同名称。 使用 **“显示源名称”** 命令可以看到子级别从其复制的列。  
  
#### <a name="to-show-a-source-name"></a>显示源名称  
  
-   右键单击某一层次结构子级别，然后单击“显示源名称”。 此时将显示该子级别从其复制的列的名称。  
  
##  <a name="bkmk_delete"></a> 删除层次结构  
  
#### <a name="to-delete-a-hierarchy-and-remove-its-child-levels"></a>删除层次结构及其子级别  
  
-   右键单击父层次结构级别，然后单击“删除层次结构”。  
  
-   或者，单击父层次结构级别，然后按 Delete 键。 这也会删除其所有子级别。  
  
## <a name="see-also"></a>请参阅  
 [表格模型设计器&#40;SSAS 表格&#41;](../tabular-model-designer-ssas-tabular.md)   
 [层次结构（SSAS 表格）](hierarchies-ssas-tabular.md)   
 [度量值（SSAS 表格）](measures-ssas-tabular.md)  
  
  
