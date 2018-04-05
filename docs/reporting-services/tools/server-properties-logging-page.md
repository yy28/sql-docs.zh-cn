---
title: 服务器属性（“日志记录”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 58e911ede9b388f31c3aeda76e44d8bec0fbdf1c
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="server-properties-logging-page"></a>服务器属性（“日志记录”页）
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的此 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 页可以对报表服务器收集的报表执行数据设置限制。 执行数据存储在报表服务器数据库内部。 可以跟踪在本机模式或 SharePoint 集成模式下运行的报表服务器的报表活动。 如果报表服务器是扩展部署的一部分，则报表执行日志会将有关整个部署内所有报表活动的记录保存到一个日志文件中。  
  
 若要打开此页，请执行以下操作：
 1) 开始 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) 连接到报表服务器。
 3) 右键单击报表服务器名称，然后选择“属性”。 
 4) 单击 **“日志记录”** 将此页打开。  
  
## <a name="options"></a>“常规”  
 **启用报表执行日志记录**  
 单击此选项可创建和存储有关服务器上报表活动的信息。 如果启用此选项，则报表服务器将跟踪已使用的报表、报表的处理频率、已执行的报表操作的类型、输出格式和运行报表的人员。 有关在该日志中捕获的其他数据点的详细信息，请参阅 [报表服务器 ExecutionLog 和 ExecutionLog3 视图](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 **删除保留时间超过以下天数的日志条目**  
 指定天数，报表执行日志中超过此天数的日志条目将被切除。 默认值为 60 天。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [报表服务器 ExecutionLog 和 ExecutionLog3 视图](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
