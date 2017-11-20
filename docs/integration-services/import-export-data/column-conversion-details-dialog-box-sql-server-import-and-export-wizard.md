---
title: "列转换详细信息对话框 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 985ba8a478999a153b3bb32649b98c3e809fc5e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>“列转换详细信息”对话框（SQL Server 导入和导出向导）
  如果双击“查看数据类型映射”  页上的单个列的行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “导入和导出向导”会显示“列转换详细信息”  对话框。 在此页上你可以查看有关单个列的详细转换信息。 信息包括以下各项：
-   在源和目标列的数据类型。
-   数据类型转换，以将该向导将执行，如果转换是必需的。
-   向导用于确定所需的数据类型转换的数据类型映射文件。 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>“列转换详细信息”页的屏幕截图 
 下面的屏幕截图显示用户双击“查看数据类型映射”  页上的行后，向导的“列转换详细信息”  对话框。 若要进一步了解“查看数据类型映射”  页，请参阅 [查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。
 
在此示例中，你将看到以下操作。
-   `PersonID`源 SQL Server 表中的列的类型是`int`。 向导将此类型映射到 SQL Server Integration Services (SSIS)`DT_I4`数据类型，这是特意引用数据类型映射文件 MSSQLToSSIS10.xml 4 字节有符号的整数。
-   `PersonID`目标 SQL Server 表中的列的类型也是`int`。 向导将映射到此类型具有相同的 SSIS 数据类型。
-   在向导结束时已经，*此列不需要转换*。
 
  
 ![导入和导出向导中的列转换页](../../integration-services/import-export-data/media/column-conversion.png "列转换页导入和导出向导") 
  
## <a name="whats-next"></a>下一步是什么？  
 查看列转换详细信息并单击“确认” 后，“列转换详细信息”  对话框将返回到“查看数据类型映射”  页。 有关详细信息，请参阅 [查看数据类型映射](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另请参阅
[SQL Server 导入和导出向导中的数据类型映射](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

