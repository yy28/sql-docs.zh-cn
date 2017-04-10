---
title: "合并数据（用于 Excel 的 MDS 外接程序） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 合并数据（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，当你在发布前想要比较数据时，合并来自两个工作表的数据。 在此过程中，您将来自两个工作表中的数据合并到一个工作表中。 然后可以进行进一步的比较，并确定哪些数据（如果有）将发布到 MDS 存储库。  
  
## 先决条件  
  
-   必须具有包含 MDS 管理的数据的工作表。 有关详细信息，请参阅 [数据导出到 Excel 从 Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)。  
  
-   必须具有包含要与 MDS 管理的数据合并的数据的工作表。 此工作表必须具有标题行。  
  
### 将非托管数据合并到 MDS 管理的工作表  
  
1.  在包含 MDS 管理的数据中的表上 **发布并验证** 组中，单击 **合并数据**。  
  
2.  在 **“合并数据”** 对话框中的 **“要与 MDS 数据组合的范围”** 文本框旁，单击图标。 该对话框将收缩。  
  
3.  单击包含要合并的数据的工作表。  
  
4.  突出显示工作表上要合并的所有单元，包括标题行。  
  
5.  在 **“合并数据”** 对话框中，单击图标。 该对话框将展开。  
  
6.  对于为 MDS 实体列出的列，选择 **“相应列”**下的列。 所有 MDS 列都不需要相应列。  
  
7.  单击 **“合并”**。 **SOURCE** 列将显示，指示数据是来自 MDS 还是外部源。  
  
## 后续步骤  
  
-   若要查找的 MDS 托管和外部数据之间的相似之处，请参阅 [匹配相似数据 & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)。  
  
## 另请参阅  
 [概述︰ 将数据导出到 Excel & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [用于 Excel 的 MDS 外接程序中的数据质量匹配](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  