---
title: 任务2：将 Excel 列映射到 DQS 域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f347cc92-950f-4021-b7af-393640dfe821
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29d45e06dcd3e67af3abbc6b356d44877e40f46b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484706"
---
# <a name="task-2-mapping-excel-columns-to-dqs-domains"></a>任务 2：将 Excel 列映射到 DQS 域
    
1.  在“映射” **** 页中，为“数据源” **** 选择“Excel 文件” ****。  
  
2.  单击 "**浏览**"，选择 "**供应商 .xlsx**"，并单击 "**打开**"。  
  
3.  选择**工作表**的**IncomingSuppliers $** 。  
  
4.  映射列，如下面的表格和屏幕快照中所示。 创建**状态**域的映射时，单击位于列表上方的工具栏上的 "**添加列映射**" 按钮。  
  
    > [!TIP]  
    >  你未使用**供应商 ID**列/域进行清理。 稍后将在匹配活动中使用**供应商 ID**域。  
  
    |Excel 列|DQS 域|  
    |------------------|----------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|联系人电子邮件|  
    |Address Line|Address Line|  
    |城市|城市|  
    |State|State|  
    |国家/地区（单击 " **+" （添加列映射）** 工具栏以添加行）|国家/地区|  
    |Zip Code|Zip|  
  
     ![Excel 列到域的映射](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-01.jpg "Excel 列到域的映射")  
  
5.  在 "**地址验证**" 复合域中映射了所有各个域后，复合域会自动参与清理过程。 单击 "**查看/选择复合域**" 按钮，查看是否自动选择了 "**地址验证**" 复合域，然后单击 **"确定"**。  
  
     ![“查看/选择复合域”对话框](../../2014/tutorials/media/et-mappingexcelcolumnstodqsdomains-02.jpg "“查看/选择复合域”对话框")  
  
6.  单击 "**下一步**" 切换到 "**清理**" 页。  
  
## <a name="next-step"></a>下一步  
 [任务 3：对照 Suppliers 知识库清理数据](../../2014/tutorials/task-3-cleansing-data-against-the-suppliers-knowledge-base.md)  
  
  
