---
title: 将数据从 MDS 加载到 Excel |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8bee7252d1adfcce827eadbd62cb7d38416d7596
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026784"
---
# <a name="load-data-from-mds-into-excel"></a>将数据从 MDS 加载到 Excel
  在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，若要使用它，必须从 MDS 存储库加载数据。  
  
 如果你想要筛选之前加载数据集，请参阅[再加载筛选器数据&#40;MDS add-in for Excel&#41; ](filter-data-before-exporting-mds-add-in-for-excel.md)相反。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
### <a name="to-load-data-from-mds-into-excel"></a>将数据从 MDS 加载到 Excel  
  
1.  打开 Excel，在 **“主数据”** 选项卡上连接到 MDS 存储库。 有关详细信息，请参阅[连接到 MDS 存储库（用于 Excel 的 MDS 外接程序）](connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **“主数据资源管理器”** 窗格中，选择所需模型和版本。 随之填充实体列表。  
  
    -   如果 **“主数据资源管理器”** 窗格不可见，请在 **“连接并加载”** 组中，单击 **“显示资源管理器”**。  
  
    -   如果 **“主数据资源管理器”** 窗格被禁用，则是因为现有工作表中已包含 MDS 管理的数据。 若要启用该窗格，请打开一个新工作表。  
  
3.  在“主数据资源管理器”窗格的实体列表中，双击要加载的实体。  
  
    > [!NOTE]  
    >  -   只有前一百万个成员才能加载到 Excel 中。 若要在加载前对列表进行筛选，请在 **“连接并加载”** 组中，单击 **“筛选器”**。  
    > -   在作为约束列表（基于域的属性）的列中，只加载前 25,000 个值。 您可以在 excelusersettings.config 文件（位于安装 Excel 的计算机上）的 MaximumDbaEntitySize 属性中更改该数值。 此文件位于 C:\Users 中\\< 用户\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices\\。  
  
    > [!NOTE]  
    >  使用用于 32 位 Excel 的 Microsoft Excel 外接程序加载文本分隔数据时，如果“要加载的单元计数”和“要发布的单元计数”属性均设置为最大值 1000，则将出现内存不足错误。 必须使用 64 位 Excel，才能使用“要加载的单元计数”和“要发布的单元计数”的最大值设置。  
  
## <a name="next-steps"></a>后续步骤  
 [发布到 MDS 数据从 Excel &#40;MDS add-in for Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>请参阅  
 [加载数据&#40;MDS add-in for Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [“筛选器”对话框 &#40;MDS Add-in for Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [将数据发布&#40;MDS add-in for Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  