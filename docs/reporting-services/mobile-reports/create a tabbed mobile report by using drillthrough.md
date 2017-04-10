---
title: "使用钻取功能创建选项卡式移动报表 | Reporting Services 移动报表 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 使用钻取功能创建选项卡式移动报表 | Reporting Services 移动报表
了解如何使用钻取功能和参数创建外观和行为与选项卡式报表类似的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 移动报表。

例如，在此报表中，顶部仪表的行为与选项卡类似。 单击“运输”仪表时，图表其余部分中的数据将筛选为运输数据。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

在后台，这实际上是五个单独报表的集合，每个报表都具有不同的参数，用于筛选报表以匹配在报表顶部所选的仪表。 

在本例中，首先创建五个报表，然后针对其中的每个报表，将其他四个仪表设置为分别钻取到其他四个报表中。 

此处为以上步骤的高级概括。

1. 使用五个仪表创建名为 Sales 的报表：
     - Sales
     - 运输
     - 燃料
     - 存储器
     - 杂项费用
2. 为报表创建四个副本，名为： 
     - 运输
     - 燃料
     - 存储器
     - 杂项费用
3.  在 Sales 报表中，将四个仪表中的每个仪表（除 Sales 仪表）设置为分别钻取到各自的报表。

4. 还是在 Sales 报表中，设置 Sales 仪表的 Accent 属性，使其相对于报表的其余部分更加醒目。

5.  现在，在“运输”报表中，将 Sales 仪表设置为钻取到 Sales 报表，然后将其他三个仪表设置为分别钻取到各自报表。

6. 同样，在“运输”报表中，设置“运输”仪表的 Accent 属性，使其相对于报表其余部分更加醒目。

5. 对“燃料”、“存储”和“杂项支出”报表执行相同的步骤。 







  
