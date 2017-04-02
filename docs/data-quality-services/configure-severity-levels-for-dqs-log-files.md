---
title: "为 DQS 日志文件配置严重级别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.admin.config.log.f1"
helpviewer_keywords: 
  - "严重级别"
  - "日志文件,严重级别"
  - "dqs 日志文件,严重级别"
  - "日志记录,严重级别"
  - "配置严重级别"
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 为 DQS 日志文件配置严重级别
  本主题介绍如何通过使用[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]为 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (DQS) 中的不同活动和模块配置严重级别。 严重级别定义 DQS 中发生的事件的强度。 DQS 事件具有以下严重级别，这些级别按严重程度递减列出：  
  
-   **致命**︰ 可能会导致严重/意外结果的关键的运行时错误。  
  
-   **错误**：其他运行时错误。  
  
-   **警告**：可能会导致错误的事件的有关警告。  
  
-   **信息**：与一般事件有关的并非错误或警告的信息。 例如，一个 DQS 过程已开始。  
  
-   **调试**: （详细） 有关详细信息事件。  
  
 通过为不同的 DQS 活动和模块配置严重级别，可筛选要记入日志的信息，以及筛选要为各 DQS 活动或模块写入 DQS 日志文件的信息。 例如，如果设置为某一 DQS 活动的严重级别 **，则发出警告**, 仅警告和更高版本与 DQS 活动关联的严重性消息 （错误和严重） 将被记录。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须具有 DQS_MAIN 数据库的 dqs_administrator 角色，才能配置日志严重性设置。  
  
##  <a name="ConfigureActivity"></a> 在活动级别配置严重级别  
 您可以在 DQS 中为以下活动配置日志严重性设置：域管理、知识发现、匹配策略、数据清理、数据匹配和引用数据服务。 为此：  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [运行数据质量客户端应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“配置”**。  
  
3.  接下来，单击 **“日志设置”** 选项卡。 下面的 DQS 活动列出可以为其选择的严重级别︰ **域管理**, ，**知识发现**, ，**清理项目 （不包括RDS)**, ，**匹配策略和匹配项目**, ，和 **RDS**。  
  
4.  对于某一 DQS 活动，选择您要记入日志的严重级别。 您可以选择下列级别之一： **“严重”**、 **“错误”**、 **“警告”**、 **“信息”**和 **“调试”**。 例如，如果您想仅严重消息写入 DQS 日志文件中的知识发现活动，则选择 **严重** 在下拉列表中对 **知识发现** 活动。  
  
    > [!NOTE]  
    >  默认情况下，将为每个活动选择 **“错误”** 。 这意味着，默认情况下对于每个活动，错误和严重消息将写入 DQS 日志文件。  
  
5.  单击 **“关闭”**。  
  
##  <a name="ConfigureModule"></a> 在模块级别配置严重级别（高级）  
 通过 **“日志设置”** 选项卡中的 **“高级”** 部分，您可以在模块级别配置日志严重性设置。 模块是在 DQS 中的某一特性内实现不同功能的 DQS 系统程序集。 例如，域管理活动包含不同功能，例如定义域规则、定义规则条件、为复合域定义跨域规则等。  
  
 有时，活动级别的粒度级别是不足够的。 您可能要调查某个活动内的特定模块中发生的问题。 它有助于选择在模块级别配置日志严重级别，以便更准确地隔离和跟踪问题。  
  
 在活动级别指定的日志严重性设置将确定构成该活动的所有模块的日志严重性设置。 但是，如果在活动级别和模块级别上的日志严重性设置之间存在任何冲突，则应考虑模块级别的严重性设置。  
  
> [!NOTE]  
>  -   默认情况下，在 **“高级”** 部分中预先配置 **Microsoft.Ssdqs.Core.Startup** ，并且严重级别设置为 **“信息”**。 这样可使与启动和停止 DQS 服务相关的严重级别为“信息”和更高（“警告”、“错误”和“严重”）的事件记入日志。  
> -   只有在您是熟悉 DQS 系统程序集的高级 DQS 用户的情况下，才应在模块级别配置日志严重级别。  
  
 在模块级别配置日志严重级别：  
  
1.  在 **“日志设置”** 选项卡上，单击针对 **“高级”** 的向下箭头以便显示该区域。  
  
2.  在网格中显示，从下拉列表中选择一个模块名称 **模块** 列。  
  
3.  接下来，从下拉列表中选择该模块的严重级别 **严重性** 列。 您可以选择下列级别之一： **“严重”**、 **“错误”**、 **“警告”**、 **“信息”**和 **“调试”**。  
  
     例如，在域管理活动内，您可以通过选择 **Microsoft.Ssdqs.DomainRules.Define** 模块，然后选择不同的日志严重级别，为域规则定义功能设置与域管理活动不同的粒度级别。 同样，可以通过选择设置跨域规则功能不同的粒度级别 **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** 模块，然后选择不同的日志严重级别。  
  
4.  如果需要，为其他模块重复步骤 2 和 3。 您还可以通过单击 **“添加模块”** 和 **“删除模块”** 图标，向网格中添加或删除行。  
  
5.  单击 **“关闭”**。  
  
## 另请参阅  
 [为 DQS 日志文件配置高级设置](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  