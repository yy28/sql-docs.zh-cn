---
title: 级别和成员（"浏览器" 选项卡，维度设计器）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.browsertab.levelsandmembers.f1
ms.assetid: 3f61e384-5b4e-4480-a7ed-b408de2fdea7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad602710cab83e2be25a03a4da6cce0c3407493e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078113"
---
# <a name="level-and-members-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>级别和成员（“浏览器”选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用此窗格浏览当前选择的层次结构和语言的成员。 若要选择要浏览的层次结构或语言，请使用 **“工具栏”** 窗格上的 **“层次结构”** 和 **“语言”** 选项。 有关工具栏窗格的详细信息，请参阅[toolbar &#40;浏览器选项卡，维度设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)。  
  
## <a name="writeback-mode"></a>写回模式  
 如果启用了写回模式，此窗格的功能将会更改。 所选的维度必须启用写操作（即维度的 `WriteEnabled` 属性必须设置为 True），并且维度必须部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例，以便启用写回模式。  
  
 若要启用写回模式，可以从“工具栏”**** 窗格中选择“写回”****，或者右键单击“级别和成员”**** 窗格，从上下文菜单中选择“写回”****。  
  
 如果启用了写回模式，您可以在 **“级别和成员”** 窗格中执行以下其他操作：  
  
|任务|执行|  
|-----------|-------------|  
|在所选的层次结构中创建同级成员和子成员。|右键单击所选的成员，从上下文菜单中选择“创建同级”**** 可以创建同级成员，或选择“创建子级”**** 可以创建子成员。|  
|在层次结构中上下移动所选成员。|将所选的成员拖动到适合的父成员或子成员中，或者单击 **“工具栏”** 窗格上的 **“增加缩进”** 或 **“减少缩进”** ，上下移动所选成员的层次结构级别。|  
|重命名所选的成员。|右键单击所选的成员，选择“重命名”****，或单击已经选择的成员。|  
|编辑成员的属性值。|双击所选成员的所选成员属性的值，并编辑此值。|  
  
## <a name="options"></a>选项  
 **当前级别**  
 显示当前在“树”**** 中所选成员所属的级别。  
  
 **视图**  
 显示当前所选的层次结构和语言的成员。  
  
 如果在工具栏窗格的 **“成员属性”** 选项中选择了成员属性，那么每个成员的属性将显示为一列。  
  
 如果启用了写回模式，则对于与维度中键属性相关联的每个键列，都将显示一列。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击所选成员的“级别和成员”**** 窗格中的任意部分后，你可以从显示的上下文菜单中选择以下选项：  
  
 **创建同级**  
 在所选成员的同一级别上创建新的成员。  
  
> [!NOTE]  
>  只有所选的成员不是处于“（全部）”级别的成员时，才会启用此选项。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **创建子级**  
 在所选成员的下一级别创建新的成员，作为所选成员的子成员。  
  
> [!NOTE]  
>  只有选择了非最低级别的成员，才启用此选项。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **剪切**  
 将所选成员复制到剪贴板，并且从层次结构中删除所选成员。  
  
> [!NOTE]  
>  只有所选的成员不是处于“全部”级别的成员时，才启用此选项。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **粘贴**  
 将之前使用“剪切”**** 删除的成员粘贴到所选成员后紧邻的位置。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **删除**  
 从层次结构中删除所选的成员。  
  
> [!NOTE]  
>  只有所选的成员不是处于“全部”级别的成员时，才启用此选项。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **重命名**  
 选择此项可以编辑所选成员的名称。  
  
> [!NOTE]  
>  只有所选的成员不是处于“全部”级别的成员时，才启用此选项。  
  
> [!NOTE]  
>  只有启用了写回模式，才会显示此选项。  
  
 **筛选成员**  
 显示“筛选成员”**** 对话框，以便筛选所选层次结构的“级别和成员”**** 中所显示的成员。 有关“筛选成员”**** 对话框的详细信息，请参阅[“筛选成员”对话框（Analysis Services - 多维数据）](filter-members-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **全部展开**  
 展开“树”**** 中的所有成员。  
  
> [!NOTE]  
>  只有选择了非最低级别的成员，才启用此选项。  
  
 **全部折叠**  
 折叠“树”**** 中的所有成员。  
  
 **展开成员**  
 展开“树”**** 中所选的成员。  
  
 **折叠成员**  
 折叠“树”**** 中所选的成员。  
  
 **写回**  
 选择此项将启用写回模式。  
  
## <a name="see-also"></a>另请参阅  
 [工具栏 &#40;浏览器选项卡，维度设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [&#41; &#40;Analysis Services 多维&#41;数据的浏览器 &#40;维度设计器](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
