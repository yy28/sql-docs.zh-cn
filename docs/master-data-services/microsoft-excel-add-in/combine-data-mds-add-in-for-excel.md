---
title: "合并数据 （MDS 外接程序 excel） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 87457a33b1fd66f42baab7ea59dbaa9c2f2123df
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="combine-data-mds-add-in-for-excel"></a>合并数据（用于 Excel 的 MDS 外接程序）
  在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，合并来自两个工作表的数据，当你想要在发布前的数据进行比较。 在此过程中，您将来自两个工作表中的数据合并到一个工作表中。 然后可以进行进一步的比较，并确定哪些数据（如果有）将发布到 MDS 存储库。  
  
## <a name="prerequisites"></a>必要條件  
  
-   必须具有包含 MDS 管理的数据的工作表。 有关详细信息，请参阅 [从 Master Data Services 中将数据导出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)。  
  
-   必须具有包含要与 MDS 管理的数据合并的数据的工作表。 此工作表必须具有标题行。  
  
### <a name="to-combine-non-managed-data-into-an-mds-managed-sheet"></a>将非托管数据合并到 MDS 管理的工作表  
  
1.  在包含 MDS 管理的数据的工作表上，在 **“发布并验证”** 组中，单击 **“合并数据”**。  
  
2.  在 **“合并数据”** 对话框中的 **“要与 MDS 数据组合的范围”** 文本框旁，单击图标。 该对话框将收缩。  
  
3.  单击包含要合并的数据的工作表。  
  
4.  突出显示工作表上要合并的所有单元，包括标题行。  
  
5.  在 **“合并数据”** 对话框中，单击图标。 该对话框将展开。  
  
6.  对于为 MDS 实体列出的列，选择 **“相应列”**下的列。 所有 MDS 列都不需要相应列。  
  
7.  单击 **“合并”**。 **SOURCE** 列将显示，指示数据是来自 MDS 还是外部源。  
  
## <a name="next-steps"></a>后续步骤  
  
-   若要查找的 MDS 管理的和外部的数据之间的相似之处，请参阅[匹配相似数据 &#40;MDS add-in for Excel &#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>另请参阅  
 [概述：将数据导出到 Excel（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [用于 Excel 的 MDS 外接程序中的数据质量匹配](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  
