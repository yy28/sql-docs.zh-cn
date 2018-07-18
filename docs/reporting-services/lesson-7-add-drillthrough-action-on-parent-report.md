---
title: 第 7 课：在父报表上添加钻取操作 | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: aad2da1a-d7b1-4afa-a66a-1ff102e8306f
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: afb72e601ef9715cf0951cbff46c1033aa1c1854
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33015284"
---
# <a name="lesson-7-add-drillthrough-action-on-parent-report"></a>第 7 课：在父报表上添加钻取操作
向网站应用程序添加 ReportViewer 控件后，接下来要在父报表上添加钻取操作。  
  
### <a name="to-add-drillthrough-action-on-the-parent-report"></a>在父报表上添加钻取操作  
  
1.  转到父报表。  
  
2.  选择包含“名称”值的文本框。  
  
3.  右键单击该文本框，然后选择“文本框属性”。  
  
4.  转到“操作”选项卡，然后选择“转到报表”选项。  
  
5.  在“指定报表”部分中输入子报表的名称。  
  
    > [!NOTE]
    > 请勿包括报表名称的文件扩展名。  
  
6.  在“使用这些参数运行报表”部分下，单击“添加”。  
  
7.  在“名称”框中键入“productid”，然后在“值”下拉列表中选择“ProductID”。  
  
8.  单击“确定”完成操作。  
  
## <a name="next-task"></a>下一个任务  
您已成功地在父报表上添加了钻取操作。 接下来，将创建一个数据筛选器，用于为子报表定义的数据表。 请参阅 [第 8 课：创建数据筛选器](../reporting-services/lesson-8-create-a-data-filter.md)。  
  
  
  

