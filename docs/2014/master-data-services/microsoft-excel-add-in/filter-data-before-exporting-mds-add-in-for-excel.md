---
title: (MDS add-in for Excel) 加载前筛选数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 277b5ff1e575f223b78f958e26801e7b209d05d5
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478927"
---
# <a name="filter-data-before-loading-mds-add-in-for-excel"></a>加载前筛选数据（用于 Excel 的 MDS 外接程序）
  在中[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，当你想要限制的大小或要加载到 Excel 的数据的作用域筛选数据。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
### <a name="to-filter-data-before-loading"></a>加载前筛选数据  
  
1.  打开 Excel，在 **“主数据”** 选项卡上连接到 MDS 存储库。 有关详细信息，请参阅[连接到 MDS 存储库（用于 Excel 的 MDS 外接程序）](connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **“主数据资源管理器”** 窗格中，选择所需模型和版本。 随之填充实体列表。  
  
    -   如果 **“主数据资源管理器”** 窗格不可见，请在 **“连接并加载”** 组中，单击 **“显示资源管理器”**。  
  
    -   如果 **“主数据资源管理器”** 窗格被禁用，则是因为现有工作表中已包含 MDS 管理的数据。 若要启用该窗格，请打开一个新工作表。  
  
3.  在 **“主数据资源管理器”** 窗格的实体列表中，单击要筛选的实体。  
  
4.  在功能区上的 **“连接并加载”** 组中，单击 **“筛选器”**。  
  
5.  通过选择要显示的属性（列）、设置列顺序，以及按需筛选数据以便返回较少行，完成填写 **“筛选器”** 对话框。 查看 **“摘要”** 窗格了解将返回的数据量。 有关详细信息，请参阅[“筛选器”对话框 &#40;MDS Add-in for Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  单击 **“加载数据”**。 将使用 MDS 管理的数据填充工作表。  
  
    > [!NOTE]  
    >  -   只有前一百万个成员才能加载到 Excel 中。  
    > -   在作为约束的列表 （基于域的属性） 的列，加载仅前 1000 个的值。  
  
## <a name="next-steps"></a>后续步骤  
 [数据从 Excel 发布到 MDS &#40;MDS add-in for Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>请参阅  
 [加载数据&#40;MDS add-in for Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [“筛选器”对话框 &#40;MDS Add-in for Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [对列重新排序（用于 Excel 的 MDS 外接程序）](reorder-columns-mds-add-in-for-excel.md)  
  
  
