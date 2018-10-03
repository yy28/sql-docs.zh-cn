---
title: 对列重新排序 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7d253acd60923b28b12f4c285f1b84f7620b524e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48071637"
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>对列重新排序（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，你可以在加载前先通过筛选列表对列重新排序。  
  
 当您在 **“筛选器”** 对话框中对属性重新排序后，数据将以新顺序加载到 Excel 中。 但是，下次筛选属性数据时，顺序将恢复为原始设计中的顺序。 若要永久更改该顺序，管理员应该在主数据管理器的 **“系统管理”** 区域中更改该顺序。 有关详细信息，请参阅 [Change the Order of Attributes](../change-the-order-of-attributes.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
### <a name="to-reorder-mds-managed-columns"></a>对 MDS 管理的列重新排序  
  
1.  打开 Excel，在 **“主数据”** 选项卡上连接到 MDS 存储库。 有关详细信息，请参阅[连接到 MDS 存储库（用于 Excel 的 MDS 外接程序）](connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **“主数据资源管理器”** 窗格中，选择所需模型和版本。 随之填充实体列表。  
  
    -   如果 **“主数据资源管理器”** 窗格不可见，请在 **“连接并加载”** 组中，单击 **“显示资源管理器”**。  
  
    -   如果 **“主数据资源管理器”** 窗格被禁用，则是因为现有工作表中已包含 MDS 管理的数据。 若要启用该窗格，请打开一个新工作表。  
  
3.  在 **“主数据资源管理器”** 窗格中，单击一个实体。  
  
4.  在 **“连接并加载”** 组中，单击 **“筛选器”**。  
  
5.  在 **“筛选器”** 对话框 **“列”** 部分的属性列表中，单击要移动的属性。  
  
6.  在列表右侧，单击 **上** 箭头或 **下** 箭头，在工作表中左右移动该属性。  
  
7.  对于每个属性重复步骤 7，直到从上到下的顺序表示您想在工作表中呈现的从左到右的顺序。  
  
8.  单击 **“加载数据”**。 工作表将使用 MDS 管理的数据填充，且列按您指定的顺序显示。  
  
## <a name="see-also"></a>请参阅  
 [加载数据&#40;MDS add-in for Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
