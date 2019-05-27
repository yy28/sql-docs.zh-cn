---
title: 服务器属性（“日志记录”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099532"
---
# <a name="server-properties-logging-page"></a>服务器属性（“日志记录”页）
  使用此页可以对报表服务器收集的报表执行数据设置限制。 执行数据存储在报表服务器数据库内部。 可以跟踪在本机模式或 SharePoint 集成模式下运行的报表服务器的报表活动。 如果报表服务器是扩展部署的一部分，则报表执行日志会将有关整个部署内所有报表活动的记录保存到一个日志文件中。  
  
 若要打开此页上，启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器，右键单击报表服务器名称，并选择**属性**。 单击 **“日志记录”** 将此页打开。  
  
## <a name="options"></a>选项  
 **启用报表执行日志记录**  
 单击此选项可创建和存储有关服务器上报表活动的信息。 如果启用此选项，则报表服务器将跟踪已使用的报表、报表的处理频率、已执行的报表操作的类型、输出格式和运行报表的人员。 在日志中捕获的其他数据点的详细信息，请参阅[报表服务器执行日志和 ExecutionLog3 视图](../report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 **删除保留时间超过以下天数的日志条目**  
 指定天数，报表执行日志中超过此天数的日志条目将被切除。 默认值为 60 天。  
  
## <a name="see-also"></a>请参阅  
 [设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 日志文件和来源](../report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio 中报表服务器的 F1 帮助](report-server-in-management-studio-f1-help.md)   
 [报告服务器执行日志和 ExecutionLog3 视图](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
