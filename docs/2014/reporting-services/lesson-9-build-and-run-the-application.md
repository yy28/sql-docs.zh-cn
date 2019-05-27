---
title: 第 9 课：生成并运行应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 321075631a48570a80e8294f992e8ddb17d50bd3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108375"
---
# <a name="lesson-9-build-and-run-the-application"></a>第 9 课：生成并运行应用程序
  创建用于数据表的数据筛选器后，接下来要生成并运行网站应用程序。  
  
### <a name="to-build-and-run-the-application"></a>生成并运行应用程序  
  
1.   按 CTRL+F5 以运行 Default.aspx 页但不调试，或按 F5 以运行该页并进行调试。  
  
      在生成过程中，将编译报表，并将所发现的任何错误（如报表所使表达式中的语法错误）添加到位于 Visual Studio 窗口底部的“任务列表”。  
  
     在浏览器中显示该网页。 ReportViewer 控件显示报表。 可使用工具栏在报表中浏览、进行缩放以及将报表导出到 Excel。  
  
2.   将鼠标悬停在“名称”列下的任意行上方。 鼠标光标将显示一个手形符号。  
  
3.   单击“名称”列中的某个值。 随后将显示子报表以及经过筛选的相应数据。  
  
4.  单击“返回父报表”  图标，在 **ReportViewer** 工具栏中导航回父报表。  
  
     ![ssrs 钻取使用 ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "ssrs 钻取使用 ReportViewer")  
  
5.  关闭浏览器以退出。  
  
  
