---
title: 查看 Integration Services 服务的事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57340afcbe1914b5e54ded06c8a7384ff33fd901
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420134"
---
# <a name="view-events-for-the-integration-services-service"></a>查看 Integration Services 服务的事件
  可以使用以下两个工具来查看 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的事件：  
  
-   **中的** “日志文件查看器” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]对话框。 **“日志文件查看器”** 对话框包括导出、筛选和搜索日志的选项。 有关“日志文件查看器”**** 中选项的详细信息，请参阅[日志文件查看器 F1 帮助](../relational-databases/logs/log-file-viewer-f1-help.md)。  
  
-   Windows 事件查看器。  
  
 有关由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务记录的事件的说明，请参阅 [由 Integration Services 服务记录的事件](service/events-logged-by-the-integration-services-service.md)。  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中查看 Integration Services 的服务事件  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **“文件”** 菜单上，单击 **“连接对象资源管理器”**。  
  
3.  在 **“连接到服务器”** 对话框中，选择 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器类型，选择或找到要连接到的服务器，然后单击 **“连接”**。  
  
4.  在对象资源管理器中，右键单击 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]，再单击“查看日志”****。  
  
5.  若要查看 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 事件，请选择 **SQL Server Integration Services**。 如果选择或清除 **SQL Server Integration Services** 选项，则会同时选择或清除 **“NT 事件”** 选项。  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>在 Windows 事件查看器中查看 Integration Services 的服务事件  
  
1.  在 **“控制面板”** 中，如果使用的是经典视图，请单击 **“管理工具”**；如果使用的是分类视图，请单击 **“性能和维护”** ，再单击 **“管理工具”**。  
  
2.  单击 **“事件查看器”**。  
  
3.  在 **“事件查看器”** 对话框中，单击 **“应用程序”**。  
  
4.  在“应用程序”**** 管理单元中，找到“源”**** 列中具有值 **SQLISService** 的项，右键单击该项，再单击“属性”****。  
  
5.  可以选择单击向上键或向下键来显示上一个事件或下一个事件。  
  
6.  可以选择单击“复制到剪贴板”图标来复制事件信息。  
  
7.  选择使用字节或字来显示事件数据。  
  
8.  单击" **确定**"。  
  
9. 在 **“文件”** 菜单上，单击 **“退出”** 关闭 **“事件查看器”** 对话框。  
  
## <a name="see-also"></a>另请参阅  
 [管理 Integration Services 服务](../../2014/integration-services/manage-the-integration-services-service.md)   
 [添加数据流性能计数器的日志](performance/performance-counters.md)  
  
  
