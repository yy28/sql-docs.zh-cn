---
title: "Integration Services 服务器的报告 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1"
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Integration Services 服务器的报告
  在当前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了标准报告，帮助你监视部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。 这些报告有助于您查看包状态和历史记录，并根据需要确定包执行失败的原因。  
  
 在每个报告页的顶部，后退图标会将您转到查看过的上一页，刷新图标会刷新在该页上显示的信息，打印图标则可以打印当前页。  
  
 有关将包部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的详细信息，请参阅[将项目部署到 Integration Services 服务器](../../integration-services/packages/deploy-projects-to-integration-services-server.md)。  
  
## Integration Services 面板  
 **“Integration Services 面板”** 报告提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上所有包执行的概览。 对于已在服务器上运行的每个包，该面板允许您“放大”以便查找有关可能已发生的包执行错误的具体细节。  
  
 该报告显示以下信息部分。  
  
|部分|Description|  
|-------------|-----------------|  
|**执行信息**|显示过去 24 小时内处于不同状态（失败、正在运行、成功、其他）的执行次数。|  
|**包信息**|显示过去 24 小时内执行的包总数。|  
|**连接信息**|显示过去 24 小时内失败的执行中使用的连接。|  
|**包详细信息**|显示过去 24 小时内发生的已完成执行的详细信息。 例如，本节说明了失败的执行次数与执行总次数，执行的持续时间（秒）和过去三个月内执行的平均持续时间。<br /><br /> 通过单击 **“概述”**、 **“所有消息”**和 **“执行性能”**，可以查看有关包的其他信息。<br /><br /> **“执行性能”** 报告显示上次执行实例的持续时间、开始和结束时间以及应用的环境。<br /><br /> **“执行性能”** 报告中包含的图表和关联的表显示过去 10 次成功执行包的持续时间。 该表还显示过去三个月内的平均执行持续时间。 在运行时可能会为这 10 次成功执行包应用不同的环境和不同的文字值。<br /><br /> 最后， **“执行性能”** 报告显示包数据流组件的活动时间和总时间。 活动时间指组件在所有阶段中用于执行的总共用时，而总时间指示组件占用的总时间。 如果上次包执行的日志记录级别设置为“性能”或“详细”，则该报告仅显示包组件的此信息。<br /><br /> **“概述”** 报告显示包任务的状态。 **“消息”** 报告显示包和任务的事件消息和错误消息，如报告开始和结束时间，以及写入的行数。<br /><br /> 还可以单击 **“概述”** 报告中的 **“查看消息”** ，导航到 **“消息”** 报告。 还可以单击 **“消息”** 报告中的 **“查看概述”** ，导航到 **“概述”** 报告。|  
  
 您可以通过单击 **“筛选器”** ，然后在 **“筛选设置”** 对话框中选择条件，对在任何页上显示的表进行筛选。 可用的筛选条件依赖于要显示的数据。 您可以通过在 **“筛选设置”** 对话框中单击排序图标，更改报告的排序顺序。  
  
## “所有执行”报告  
 **“所有执行”** 报告显示已在服务器上执行的所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 执行的摘要。 可以存在示例包的多个执行。 与 **“Integration Services 面板”** 报告不同，您可以配置 **“所有执行”** 报告以显示在日期范围内开始的执行。 该日期可以跨多天、多月或多年。  
  
 该报告显示以下信息部分。  
  
|部分|Description|  
|-------------|-----------------|  
|筛选|显示应用于该报告的当前筛选器，如开始时间范围。|  
|执行信息|显示每个包执行的开始时间、结束时间和持续时间。您可以查看用于包执行的参数值列表，如使用“执行包”任务传递给子包的值。 若要查看参数列表，请单击“概述”。|  
  
 有关使用执行包任务使值可用于子包的详细信息，请参阅 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)。  
  
 有关参数的详细信息，请参阅 [Integration Services (SSIS) 包和项目参数](../../integration-services/integration-services-ssis-package-and-project-parameters.md)。  
  
## 所有连接  
 **“所有连接”** 报告提供以下有关已失败的连接的信息，有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上已发生的执行的信息。  
  
 该报告显示以下信息部分。  
  
|部分|Description|  
|-------------|-----------------|  
|“筛选器”|显示应用于此报告的当前筛选器，如具有指定字符串的连接和 **“上次失败时间”** 范围。<br /><br /> 可以设置 **“上次失败时间”** 范围以仅显示在日期范围内发生的连接失败。 该范围可以跨多个天、月或年。|  
|详细信息|显示连接字符串、某个连接失败过程中的执行次数和上次连接失败的日期。|  
  
## “所有操作”报告  
 **“所有操作”** 报告显示已在服务器上执行的所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作的摘要，包括包部署、验证和执行以及其他管理操作。 与 Integration Services 面板一样，您可以将筛选器应用于表，以便缩小显示的信息的范围。  
  
## “所有验证”报告  
 **“所有验证”** 报告显示已在服务器上执行的所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 验证的摘要。 摘要中显示每次验证的信息，如状态、开始时间和结束时间。 每个摘要条目包含一个指向在验证期间生成的消息的链接。 与 Integration Services 面板一样，您可以将筛选器应用于表，以便缩小显示的信息的范围。  
  
## 自定义报告  
 可以将自定义报告（.rdl 文件）添加到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中“Integration Services 目录”节点下的 **SSISDB** 目录节点。 在添加报告前，请确认正在使用第三方命名约定以完全限定您引用的对象（如源表）。 否则， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将显示错误。 命名约定为 \<数据库>.\<所有者>.\<对象>。 例如，SSISDB.internal.executions。  
  
> [!NOTE]  
>  将自定义报告添加到“数据库”节点下的 **SSISDB** 节点时，可以不使用 SSISDB 前缀。  
  
 有关如何创建和添加自定义报告的说明，请参阅 [Add a Custom Report to Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)。  
  
## 相关任务  
 [查看 Integration Services 服务器的报告](../../integration-services/performance/view-reports-for-the-integration-services-server.md)  
  
## 相关内容  
[监视运行包和其他操作](../../integration-services/performance/monitor-running-packages-and-other-operations.md)
  
  