---
title: 服务器属性（“高级”页）- Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 2016-10-18
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: erikre
ms.openlocfilehash: 81c0e6a2bce527404e7c4f59c10a914e3ac938b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015167"
---
# <a name="server-properties-advanced-page---reporting-services"></a>服务器属性（“高级”页）- Reporting Services
  使用此页可以针对报表服务器设置系统属性。 可通过多种方法来设置系统属性。 此工具提供了一个图形用户界面，您不必编写代码即可设置属性。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器实例，右键单击报表服务器名称，然后选择“属性”。 单击 **“高级”** 打开此页。  
  
## <a name="options"></a>“常规”  
 **EnableMyReports**  
 指示是否启用“我的报表”功能。 值为`true`指示已启用该功能。  
  
 **MyReportsRole**  
 对用户的“我的报表”文件夹创建安全策略时所用角色的名称。 默认值是 `My Reports Role`。  
  
 **EnableClientPrinting**  
 确定是否可从报表服务器下载 RSClientPrint ActiveX 控件。 有效值为`true`和`false`。 默认值是 `true`。 有关此控件所需的其他设置的详细信息，请参阅 [启用和禁用 Reporting Services 的客户端打印](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
 **EnableExecutionLogging**  
 指示报表执行日志记录是否处于启用状态。 默认值是 `true`。 有关报表服务器执行日志的详细信息，请参阅[报表服务器执行日志和 ExecutionLog3 视图](../report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 **ExecutionLogDaysKept**  
 在执行日志中保留报表执行信息的天数。 此属性的有效值包括`-1`通过`2`，`147`，`483`，`647`。 如果值为 `-1`，则不从执行日志表中删除项。 默认值是 `60`。  
  
 **SessionTimeout**  
 会话保持活动状态的时间长度（以秒为单位）。 默认值是 `600`。  
  
 **SharePointIntegratedMode**  
 这是一个指示服务器模式的只读属性。 如果此值为 False，则报表服务器在本机模式下运行。  
  
 **SiteName**  
 在报表管理器的页面标题上显示的报表服务器站点的名称。 默认值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]秒。 此属性可以是空字符串。 最大长度为 8,000 个字符。  
  
 **StoredParametersLifetime**  
 指定所存储的参数能够保存的最大天数。 有效值为`-1`，`+1`通过`2,147,483,647`。 默认值是`180`天。  
  
 **StoredParametersThreshold**  
 指定报表服务器可以存储的参数值的最大数目。 有效值为`-1`，`+1`通过`2,147,483,647`。 默认值是 `1500`。  
  
 **UseSessionCookies**  
 指示报表服务器与客户端浏览器通信时是否应使用会话 cookie。 默认值是 `true`。  
  
 **ExternalImagesTimeout**  
 确定在连接超时之前，必须对外部映像文件检索的时间长度。默认值为 `600` 秒。  
  
 **SnapshotCompression**  
 定义如何压缩快照。 默认值是 `SQL`。 有效值如下：  
  
 **SQL =** 在存储到报表服务器数据库中时压缩快照。 这是当前的行为。  
  
 **None** = 不压缩快照。  
  
 **All =** 针对所有的存储选项（包括报表服务器数据库或文件系统）压缩快照。  
  
 **SystemReportTimeout**  
 在报表服务器命名空间中托管的所有报表的默认报表处理超时值（以秒为单位）。 该值可在报表级别进行重写。 如果设置了此属性，则超过指定时间后报表服务器会尝试停止处理报表。 有效值为`-1`通过`2`，`147`，`483`，`647`。 如果值为 `-1`，则处理期间命名空间中的报表不会超时。 默认值是 `1800`。  
  
 **SystemSnapshotLimit**  
 为报表存储的快照的最大数目。 有效值为`-1`通过`2`，`147`，`483`，`647`。 如果值为`-1`，没有任何快照限制。  
  
 **EnableIntegratedSecurity**  
 确定报表数据源连接是否支持 Windows 集成安全性。 默认值为 `True`。 有效值如下：  
  
 `True` = 启用 Windows 集成安全性。  
  
 `False` = 未启用 Windows 集成安全性。 将不运行配置为使用 Windows 集成安全性的报表数据源。  
  
 `EnableLoadReportDefinition`  
 选中此选项可以指定用户是否可以从报表生成器报表中执行特别报告执行。 设置此选项确定的值`EnableLoadReportDefinition`报表服务器上的属性。  
  
 如果清除此选项，则属性将设置为 False，报表服务器将不会为使用报表模型作为数据源的报表生成点击链接型报表。 将阻止对 LoadReportDefinition 方法的任何调用。  
  
 如果关闭此选项，则会缓解恶意用户通过用 LoadReportDefinition 请求使报表服务器重载来启动拒绝服务攻击的威胁。  
  
 **EnableRemoteErrors**  
 包括外部错误信息（例如，有关报表数据源的错误信息），其中包含针对从远程计算机请求报表的用户返回的错误消息。 有效值为`true`和`false`。 默认值是 `false`。 有关详细信息，请参阅[启用远程错误 (Reporting Services)](../report-server/enable-remote-errors-reporting-services.md)。  
  
 **EnableReportDesignClientDownload**  
 指定是否可以从报表服务器下载报表生成器安装包。 如果清除此设置，则指向报表生成器的 URL 将不起作用。 有关详细信息，请参阅 [配置报表生成器访问权限](../report-server/configure-report-builder-access.md)。  
  
 **EditSessionCacheLimit**  
 指定可在一个报表编辑会话中处于活动状态的数据缓存条目数。 默认数量为 5。  
  
 **EditSessionTimeout**  
 指定报表编辑会话超时之前的秒数。默认值为 7200 秒（2 小时）。  
  
 **EnableTestConnectionDetailedErrors**  
 指示当用户使用报表服务器测试数据源连接时，是否向客户端计算机发送详细的错误消息。 默认值是 `true`。 如果选项设置为`false`，只有一般错误消息发送。  
  
## <a name="see-also"></a>请参阅  
 [设置报表服务器属性 (Management Studio)](set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 属性](../report-server-web-service/net-framework/reporting-services-properties.md)   
 [Management Studio 中报表服务器的 F1 帮助](report-server-in-management-studio-f1-help.md)   
 [报表服务器系统属性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
 [为部署和管理任务编写脚本](script-deployment-and-administrative-tasks.md)   
 [启用和禁用“我的报表”](../report-server/enable-and-disable-my-reports.md)  
  
  