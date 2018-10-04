---
title: 任务 2： 将 Excel 列映射到 DQS 域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4af26cb52b8d30dbfad5fc5ab40dc732f8ce4dc2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135517"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>任务 2：将 Excel 列映射到 DQS 域
    
1.  在“映射”  页中，为“数据源”  选择“Excel 文件” 。  
  
2.  单击**浏览**，选择**Suppliers.xlsx**，然后单击**打开**。  
  
3.  选择**IncomingSuppliers$** 有关**工作表**。  
  
4.  映射列，如下面的表格和屏幕快照中所示。 创建映射时**状态**域中，单击**添加列映射**工具栏上的按钮位于列表正上方。  
  
    > [!TIP]  
    >  不使用**供应商 ID**列/域来进行清理。 将使用**供应商 ID**更高版本中的匹配活动的域。  
  
    |Excel 列|DQS 域|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |国家/地区 (单击 **+ （添加列映射）** 工具栏添加行)|Country|  
    |Zip Code|Zip|  
  
     ![Excel 列到域映射](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Excel 列到域的映射")  
  
5.  当您映射了中的所有域**地址验证**复合域的复合域将自动参与清理过程。 单击**查看/选择复合域**按钮以查看**地址验证**复合域，将自动选择，然后单击**确定**。  
  
     ![查看/选择复合域对话框](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "查看/选择复合域对话框")  
  
6.  单击**下一步**若要切换到**清理**页。  
  
## <a name="next-step"></a>下一步  
 [任务 3：对照 Suppliers 知识库清理数据](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
