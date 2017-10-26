---
title: "管理 DQS 日志文件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb82238a0e88b3e639a6185bb80de1dd1b33c351
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="manage-dqs-log-files"></a>管理 DQS 日志文件
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 日志文件可帮助您诊断和解决与 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]和 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]有关的问题。 为 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]和 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]生成单独的日志文件。  
  
 您可以使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 为 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 功能和模块配置日志严重性设置。 或者，您还可以通过在 DQS_MAIN 数据库中手动更改 DQS 日志配置设置以及在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 计算机上更改 XML 文件，为 DQS 日志文件配置其他一些（高级）设置。  
  
##  <a name="DQSServer"></a> 数据质量服务器日志文件  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志文件 DQServerLog.DQS_MAIN.log 包含在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上运行的活动的日志。 如果你安装了 SQL Server 的默认实例，则 DQServerLog.DQS_MAIN.log 文件将位于 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log 下。 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志文件包含以下信息部分，每个部分之间用竖线 (|) 分隔：  
  
-   日期和时间  
  
-   线程名称  
  
-   线程 ID  
  
-   日志严重性（FATAL、ERROR、WARN、INFO 和 DEBUG）  
  
    > [!NOTE]  
    >  DEBUG 日志记录严重程度与“详细”相同。  
  
-   UID（内部 DQS 基础结构 ID）  
  
-   命名空间  
  
-   类和方法  
  
-   消息  
  
 除了上述信息之外，日志文件还显示与应用程序版本、计算机名称、用户名和操作系统有关的信息。  
  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志文件中的示例条目如下：  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 DQServerLog.DQS_MAIN.log 文件是一个滚动文件，一旦现有日志文件超出在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志配置设置中指定的滚动文件大小限制，就会创建一个新的日志文件。 有关详细信息，请参阅 [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)。  
  
##  <a name="DQSClient"></a> 数据质量客户端日志文件  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志文件 DQClientLog.log 包括客户端日志。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志文件位于 %APPDATA%\SSDQS\Log。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志文件包含与服务器日志文件中相似的一组信息，但前者针对的是客户端。  
  
 与 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 日志文件一样， [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志文件也是一个滚动文件，一旦现有日志文件超出在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 日志配置设置中指定的滚动文件大小限制，就会创建一个新的日志文件。 有关详细信息，请参阅 [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)。  
  
##  <a name="DQSCleansing"></a> DQS 清理组件日志文件  
 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 日志文件 DQSSSISLog.log 包括使用 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]执行的活动的日志。 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 组件日志文件位于 %APPDATA%\SSDQS\Log。 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 日志文件包含与服务器日志文件中相似的一组信息，但前者针对的是 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]。  
  
##  <a name="RT"></a> 相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]为 DQS 日志文件配置日志严重性设置。|[为 DQS 日志文件配置严重级别](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|介绍如何为 DQS 日志文件手动配置高级设置。|[为 DQS 日志文件配置高级设置](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DQS 管理](../data-quality-services/dqs-administration.md)  
  
  

