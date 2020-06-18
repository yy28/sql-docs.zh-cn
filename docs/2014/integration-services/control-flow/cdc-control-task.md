---
title: CDC 控制任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: dc9a71c69e1b6440b5386236fa6e1f7073851b3f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919718"
---
# <a name="cdc-control-task"></a>CDC 控制任务
  CDC 控制任务用于控制变更数据捕获 (CDC) 包的生命周期。 它处理 CDC 包与初始加载包的同步以及在运行 CDC 包时处理的日志序列号 (LSN) 范围的管理。 此外，CDC 控制任务还处理错误情况和恢复。  
  
 CDC 控制任务在 SSIS 包变量中维护 CDC 包的状态，并且还可以将其保存在某一数据库表中，以便跨多个包激活和在一起执行某一公共 CDC 进程的多个包之间（例如，一个任务可负责初始加载，而另一个任务则用于滴送处理更新）维护该状态。  
  
 CDC 控制任务支持两组操作。 一组处理初始加载和更改处理的同步，另一组为 LSN 包的运行管理 CDC 的更改处理范围并且跟踪成功处理的情况。  
  
 下列操作处理初始加载和更改处理的同步：  
  
|Operation|说明|  
|---------------|-----------------|  
|ResetCdcState|此操作用于重置与当前 CDC 上下文相关联的持久的 CDC 状态。 在此操作运行后，来自 LSN-timestamp `sys.fn_cdc_get_max_lsn` 表的当前最大 LSN 将成为下一处理范围的起始范围。 此操作要求到源数据库的连接。|  
|MarkInitialLoadStart|此操作用于初始加载包的开头，以便在初始加载包开始读取源表之前记录源数据库中的当前 LSN。 此操作要求到源数据库的连接以便调用 `sys.fn_cdc_get_max_lsn`。<br /><br /> 如果在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）上工作时选择 MarkInitialLoadStart，则在连接管理器中指定的用户必须是 db_owner 或 sysadmin。|  
|MarkInitialLoadEnd|此操作用于初始加载包的末尾，以便在初始加载包完成读取源表之后记录源数据库中的当前 LSN。 此 LSN 通过以下方式确定：首先记录此操作发生时的当前时间，然后在 CDC 数据库的 `cdc.lsn_time_`mapping 表中进行查询以便查找在该时间后发生的更改。<br /><br /> 如果在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）上工作时选择 MarkInitialLoadEnd，则在连接管理器中指定的用户必须是 db_owner 或 sysadmin。|  
|MarkCdcStart|在从快照数据库生成初始加载时使用此操作。 在此情况下，更改处理应在快照 LSN 后立即开始。 您可以指定要使用的快照数据库的名称并且 CDC 控制任务将查询 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以找到快照 LSN。 您还可以选择直接指定快照 LSN。<br /><br /> 如果在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）上工作时选择 MarkCdcStart，则在连接管理器中指定的用户必须是 db_owner 或 sysadmin。|  
  
 下列操作用于管理处理范围：  
  
|Operation|说明|  
|---------------|-----------------|  
|GetProcessingRange|在调用使用 CDC 源数据流的数据流之前使用此操作。 此操作建立 CDC 源数据流在调用时读取的 LSN 的范围。 该范围存储于一个 SSIS 包变量中，在数据流处理期间 CDC 源将使用该变量。<br /><br /> 有关存储的状态的详细信息，请参阅 [定义状态变量](../data-flow/define-a-state-variable.md)。|  
|MarkProcessedRange|此操作在每次 CDC 运行后（在 CDC 数据流成功完成后）执行，以便记录在 CDC 运行中完全处理的上一个 LSN。 下一次执行 GetProcessingRange 时，此位置将是处理范围的起始位置。|  
  
## <a name="handling-cdc-state-persistency"></a>处理 CDC 状态持久性  
 此 CDC 控制任务维护激活之间的持久性状态。 在 CDC 状态中存储的信息用于确定和维护 CDC 包的处理范围以及用于检测到错误条件。 该持久性状态以字符串的形式存储。 有关详细信息，请参阅 [定义状态变量](../data-flow/define-a-state-variable.md)。  
  
 CDC 控制任务支持两种类型的状态持久性  
  
-   手动状态持久性：在此情况中，该 CDC 控制任务管理在某个包变量中存储的状态，但包开发人员必须在调用 CDC 控制前从持久性状态中读取该变量，然后在最后调用 CDC 控制并且 CDC 运行完成后将该变量写回到该持久性存储区中。  
  
-   自动状态持久性：CDC 状态存储在数据库中的表中。 该状态根据在 **“要用于存储状态的表”** 属性中命名的表中的 **StateName** 属性提供的名称存储，该表位于用于存储状态的所选连接管理器中。 默认管理器是源连接管理器，但通常的做法是使其成为目标连接管理器。 该 CDC 控制任务更新状态表中的状态值，并且该值作为环境事务的一部分提交。  
  
## <a name="error-handling"></a>错误处理  
 该 CDC 控制任务可在以下情况下报告错误：  
  
-   它无法读取持久性的 CDC 状态或者在持久性状态更新失败时。  
  
-   它无法从源数据库读取当前 LSN 信息。  
  
-   读取的 CDC 状态不一致。  
  
 在所有这些情况下，该 CDC 控制任务报告一个可以处理的错误，SSIS 可使用标准方式处理控制流错误。  
  
 在未调用标记处理的范围的情况下在另一个获取处理范围操作后直接调用获取处理范围操作时，该 CDC 控制任务还可能会报告一个警告。 这指示以前的运行失败或其他 CDC 包可能正在使用相同的 CDC 状态名称运行。  
  
## <a name="configuring-the-cdc-control-task"></a>配置 CDC 控制任务  
 可以通过 SSIS 设计器或以编程方式来设置属性。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [CDC 控制任务编辑器](../cdc-control-task-editor.md)  
  
-   [CDC 控制任务自定义属性](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [定义状态变量](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>相关内容  
  
-   social.technet.microsoft.com 上的技术文章 [安装 Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity](https://go.microsoft.com/fwlink/?LinkId=252958)。  
  
-   social.technet.microsoft.com 上的技术文章 [解决 Microsoft Change Data Capture for Oracle by Attunity 中的配置问题](https://go.microsoft.com/fwlink/?LinkId=252960)。  
  
-   social.technet.microsoft.com 上的技术文章 [解决 Microsoft Change Data Capture for Oracle by Attunity 中的 CDC 实例错误问题](https://go.microsoft.com/fwlink/?LinkId=252961)。  
  
  
