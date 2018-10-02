---
title: 导出前筛选数据 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cc58f0809f830363586390b20da29603fd1b2bcb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853265"
---
# <a name="filter-data-before-exporting-mds-add-in-for-excel"></a>导出前筛选数据 (MDS Add-in for Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，可通过筛选数据来限制要导出到 Excel 中的数据大小或范围。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
### <a name="to-filter-data-before-exporting"></a>导出前筛选数据  
  
1.  打开 Excel，在 **“主数据”** 选项卡上连接到 MDS 存储库。 有关详细信息，请参阅[连接到 MDS 存储库（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **“主数据资源管理器”** 窗格中，选择所需模型和版本。 随之填充实体列表。  
  
    -   如果 **“主数据资源管理器”** 窗格不可见，请在 **“连接并加载”** 组中，单击 **“显示资源管理器”**。  
  
    -   如果 **“主数据资源管理器”** 窗格被禁用，则是因为现有工作表中已包含 MDS 管理的数据。 若要启用该窗格，请打开一个新工作表。  
  
3.  在 **“主数据资源管理器”** 窗格的实体列表中，单击要筛选的实体。  
  
4.  在功能区上的 **“连接并加载”** 组中，单击 **“筛选器”**。  
  
5.  通过选择要显示的属性（列）、设置列顺序，以及按需筛选数据以便返回较少行，完成填写 **“筛选器”** 对话框。 查看 **“摘要”** 窗格了解将返回的数据量。 有关详细信息，请参阅[“筛选器”对话框 &#40;MDS Add-in for Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  单击 **“加载数据”**。 将使用 MDS 管理的数据填充工作表。  
  
    > [!NOTE]  
    >  -   只有前一百万个成员才能加载到 Excel 中。  
    > -   在作为约束列表（基于域的属性）的列中，默认情况下只加载前 25000 个值。  
  
## <a name="next-steps"></a>Next Steps  
 [将数据从 Excel 导入 Master Data Services（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另请参阅  
 [概述：将数据导出到 Excel（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [“筛选器”对话框 &#40;MDS Add-in for Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [对列重新排序（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  
