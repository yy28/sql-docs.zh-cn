---
title: CDC 控制任务编辑器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a87af3febdab1e98dac0b1546b8b2b8939b739d6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061119"
---
# <a name="cdc-control-task-editor"></a>CDC 控制任务编辑器
  使用 **“CDC 控制任务编辑器”** 对话框可以配置 CDC 控制任务。 CDC 控制任务配置包括定义与 CDC 数据库的连接、CDC 任务操作和状态管理信息。  
  
 若要了解有关 CDC 控制任务的详细信息，请参阅 [CDC Control Task](control-flow/cdc-control-task.md)。  
  
 **打开“CDC 控制任务编辑器”**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开包含 CDC 控制任务的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
2.  在“控制流”选项卡上，双击 CDC 控制任务。  
  
## <a name="options"></a>选项  
 **SQL Server CDC 数据库 ADO.NET 连接管理器**  
 从列表中选择现有连接管理器，或单击“新建”创建新的连接。 该连接必须是指向为 CDC 启用的并且所选更改表位于其中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的连接。  
  
 **CDC 控制操作**  
 选择要为此任务运行的操作。 所有操作都使用存储在 SSIS 包变量中的状态变量，包变量存储状态并在包的不同组件之间传递该状态。  
  
-   **标记初始加载开始**：在从不具有快照的活动数据库执行初始加载时使用此操作。 在初始加载包的开头调用此操作，以便在初始加载包开始读取源表之前记录源数据库中的当前 LSN。 此操作要求连接到源数据库。  
  
     如果你在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）时选择“标记初始加载开始”，则在连接管理器中指定的用户必须是 **db_owner** 或 **sysadmin**。  
  
-   **标记初始加载结束**：在从不具有快照的活动数据库执行初始加载时使用此操作。 在初始加载包的末尾调用此操作，以便在初始加载包完成读取源表之后记录源数据库中的当前 LSN。 此 LSN 通过以下方式确定：首先记录此操作发生时的当前时间，然后在 CDC 数据库的 `cdc.lsn_time_`映射表中进行查询以便查找在该时间后发生的更改。  
  
     如果你在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）上工作时选择“标记初始加载结束”，则在连接管理器中指定的用户必须是 **db_owner** 或 **sysadmin**。  
  
-   **标记 CDC 开始**：在从快照数据库或静默数据库执行初始加载时使用此操作。 在初始加载包内的任何一点都可以调用该操作。 该操作接受可以作为快照 LSN 的参数、快照数据库的名称（将自其自动派生快照 LSN），也可以将其保留为空（这种情况下，将当前数据库 LSN 用作更改处理包的开始 LSN）。  
  
     此操作可用来替代标记初始加载开始/结束操作。  
  
     如果你在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC（也就是说，不是 Oracle）上工作时选择“标记 CDC 开始”，则在连接管理器中指定的用户必须是 **db_owner** 或 **sysadmin**。  
  
-   **获取处理范围**：在调用使用 CDC 源数据流的数据流之前，在更改处理包中使用此操作。 此操作建立 CDC 源数据流在调用时读取的 LSN 的范围。 该范围存储于一个 SSIS 包变量中，在数据流处理期间 CDC 源将使用该变量。  
  
     有关存储的可能的 CDC 状态的详细信息，请参阅 [定义状态变量](data-flow/define-a-state-variable.md)。  
  
-   **标记已处理的范围**：在 CDC 运行结束时（在 CDC 数据流成功完成后）在更改处理包中使用此操作，以便记录在 CDC 运行中完全处理的上一个 LSN。 下一次执行 `GetProcessingRange` 时，此位置确定下一处理范围的起点。  
  
-   **重置 CDC 状态**：此操作用于重置与当前 CDC 上下文相关联的持久的 CDC 状态。 在此操作运行后，来自 LSN-timestamp `sys.fn_cdc_get_max_lsn` 表的当前最大 LSN 将成为下一处理范围的起始范围。 此操作要求到源数据库的连接。  
  
     举例来说，当您只需处理新创建的更改记录而忽略所有旧的更改记录时，就需要使用此操作。  
  
 **包含 CDC 状态的变量**  
 选择存储任务操作的状态信息的 SSIS 包变量。 在开始之前，应该先定义一个变量。 如果您选择 **“自动状态持久性”**，将自动加载和保存状态变量。  
  
 有关定义状态变量的详细信息，请参阅 [定义状态变量](data-flow/define-a-state-variable.md)。  
  
 **启动 CDC 的 SQL Server LSN/快照名称：**  
 键入自其开始执行初始加载的当前源数据库 LSN 或快照数据库的名称，以确定 CDC 的起点。 仅当 **“CDC 控制操作”** 设置为 **“标记 CDC 开始”** 时，此选项才可用。  
  
 有关这些操作的详细信息，请参阅 [CDC Control Task](control-flow/cdc-control-task.md)。  
  
 **在数据库表中自动存储状态**  
 选中此复选框后，CDC 控制任务可以在指定数据库所包含的状态表中自动加载和存储 CDC 状态。 若未选中此选项，开发人员必须在包开始执行时加载 CDC 状态，并且只要 CDC 状态发生更改就要保存该状态。  
  
 **存储状态的数据库的连接管理器**  
 从列表中选择现有 ADO.NET 连接管理器，或单击“新建”创建新的连接。 此连接指向包含状态表的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库。 状态表包含状态信息。  
  
 仅当选定 **“自动状态持久性”** 时此选项才可用，并且这是一个必需的参数。  
  
 **用于存储状态的表**  
 键入要用于存储 CDC 状态的状态表的名称。 指定的表必须具有名为 **name** 和 **state** 的两列，并且这两列的数据类型必须为 **varchar (256)**。  
  
 还可以选择 **“新建”** ，获取可生成具有必需列的新状态表的 SQL 脚本。 如果选择 **“自动状态持久性”** ，开发人员必须根据上面列出的要求创建一个状态表。  
  
 仅当选定 **“自动状态持久性”** 时此选项才可用，并且这是一个必需的参数。  
  
 **状态名称**  
 键入与持久 CDC 状态关联的名称。 使用相同 CDC 上下文的完整负载和 CDC 包将指定一个公共的状态名称。 此名称用于查找状态表中的状态行。  
  
## <a name="see-also"></a>请参阅  
 [CDC 控制任务自定义属性](control-flow/cdc-control-task-custom-properties.md)  
  
  
