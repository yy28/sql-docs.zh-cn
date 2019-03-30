---
title: 错误处理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0924c4ac6d2ddd4e14b35794b9c03ac7fb2e136
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657244"
---
# <a name="error-handling"></a>错误处理
  Oracle CDC 实例从单个 Oracle 源数据库（一个 Oracle RAC 群集被视为单个数据库）挖掘更改并且将提交的更改写入目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 CDC 数据库的更改表中。  
  
 CDC 实例在称作 **cdc.xdbcdc_state**的系统表中维护其状态。 可随时对此表进行查询以便查找 CDC 实例的状态。 有关 cdc.xdbcdc_state 表的详细信息，请参阅 [cdc.xdbcdc_state](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_state)。  
  
 下表说明 xdbcdc_state 表中的 CDC 实例状态。  
  
 对于每个状态，在 cdc.xdbcdc_state 表的相应列中将显示以下两个指示：  
  
-   实例未处于活动状态（没有当前正在处理它的 Windows 进程）。 如果“活动”列的值为 1，则处理此特定 Oracle CDC 实例的 Oracle CDC 服务的子进程正在运行。  
  
-   如果“错误”列的值为 0，则 Oracle CDC 实例未处于错误条件。 如果“错误”列的值为 1，则存在阻止 Oracle CDC 实例处理更改的错误。  
  
     如果“错误”列的值为 1 并且“活动”列的值也是 1，则对于 Oracle CDC 实例正在发生可恢复的错误，此错误可自动解决。 如果“错误”列的值为 1 并且“活动”列的值为 0，则在大多数情况下，可能需要手动解决该问题，然后处理才会恢复。  
  
 下表描述 Oracle CDC 实例可在其状态表中报告的不同的状态代码。  
  
|“登录属性”|活动状态代码|错误状态代码|“说明”|  
|------------|------------------------|-----------------------|------------------|  
|ABORTED|0|1|Oracle CDC 实例未运行。 ABORTED 子状态指示 Oracle CDC 实例曾处于活动状态但之后已意外停止。<br /><br /> ABORTED 子状态在 Oracle CDC 服务主实例检测到 Oracle CDC 实例未运行而其状态为 ACTIVE 时建立。|  
|error|0|1|Oracle CDC 实例未运行。 ERROR 状态指示 CDC 实例曾处于活动状态但之后遇到了无法恢复的错误并且禁用了自身。 ERROR 状态包含以下子状态代码：<br /><br /> MISCONFIGURED：检测到无法恢复的配置错误。<br /><br /> PASSWORD-REQUIRED：没有为适用于 Oracle 的 Attunity 更改数据捕获设计器设置密码或者配置的密码无效。 这可能是因为对服务的非对称密钥密码进行的更改。|  
|RUNNING|1|0|CDC 实例正在运行并且正在处理更改记录。 RUNNING 状态包含以下子状态代码：<br /><br /> IDLE：所有更改记录都已处理并存储在目标控制 (_CT) 表中。 没有针对控制表的活动事务。<br /><br /> PROCESSING：存在正处理、但尚未写入控制 (_CT) 表的更改记录。|  
|STOPPED|0|0|CDC 实例未在运行。 STOP 子状态指示 CDC 实例曾处于活动状态并且之后已正确停止。|  
|SUSPENDED|1|1|CDC 实例正在运行，但由于无法恢复的错误处理已挂起。 SUSPENDED 状态包含以下子状态代码：<br /><br /> DISCONNECTED：无法建立与源 Oracle 数据库的连接。 在连接恢复后会继续处理。<br /><br /> STORAGE：存储已满。 在存储变为可用时将继续处理。 在某些情况下，此状态可能不会出现，因为状态表无法更新。<br /><br /> LOGGER：记录器连接到 Oracle，但由于临时问题而无法读取 Oracle 事务日志。|  
|DATAERROR|x|x|此状态代码仅用于 **xdbcdc_trace** 表。 它不显示在 **xdbcdc_state** 表中。 具有此状态的跟踪记录指示 Oracle 日志记录存在问题。 错误日志记录以 BLOB 形式存储于“数据”列中。 DATAERROR 状态包含以下子状态代码：<br /><br /> BADRECORD：无法分析附加的日志记录。<br /><br /> CONVERT-ERROR:某些列中的数据无法转换到捕获表中的目标列。 只有在配置指定换错误应生成跟踪记录的情况下，才可能会出现此状态。|  
  
 因为 Oracle CDC 服务状态存储于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，所以，有时候数据库中的状态值可能不会反映服务的实际状态。 最常见的情形是服务丢失其与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接并且无法恢复（由于任何原因）。 在该情况下，存储在 **cdc.xdbcdc_state** 中的状态会变得陈旧。 如果上次更新时间戳 (UTC) 不止早 1 分钟，则状态可能是陈旧的。 在此情况下，使用 Windows 事件查看器可以查找与服务状态有关的附加信息。  
  
## <a name="error-handling"></a>错误处理  
 本节介绍 Oracle CDC 服务如何处理错误。  
  
### <a name="logging"></a>日志记录  
 Oracle CDC 服务在下列位置之一中创建错误信息。  
  
-   Windows 事件日志，用于记录错误以及指示 Oracle CDC 服务生命周期事件（开始、停止、连接到/重新连接到目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例）。  
  
-   MSXDBCDC.dbo.xdbcdc_trace 表，用于 Oracle CDC 服务主进程进行的一般日志记录和跟踪。  
  
-   \<cdc-database>.cdc.xdbcdc_trace 表，用于 Oracle CDC 实例进行的常规日志记录和跟踪。 这意味着与特定 Oracle CDC 实例相关的错误将记录到该实例的跟踪表中。  
  
 在对该服务执行以下操作时 Oracle CDC 服务会将信息记入日志：  
  
-   服务控制管理器启动或停止该服务。  
  
-   无法连接到关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以及在失败后成功建立连接时。  
  
-   启动 Oracle CDC 服务实例时遇到错误。  
  
-   检测到 Oracle CDC 实例已中止。  
  
-   遇到意外错误。  
  
 在对实例执行以下操作时 Oracle CDC 实例会将信息记入日志：  
  
-   启用或禁用实例。  
  
-   遇到错误。  
  
-   从可恢复的错误中恢复。  
  
 跟踪表也用来记录详细跟踪信息以便进行故障排除。  
  
### <a name="handling-source-oracle-connection-errors"></a>处理源 Oracle 连接错误  
 Oracle CDC 服务需要与源 Oracle 数据库永久连接。 许多与服务配置无关的连接错误（例如网络错误）被认为是暂时的。 因此，如果 Oracle CDC 服务无法建立与 Oracle 数据库的连接（在启动时或在断开连接后的工作期间），该服务会将其状态更改为 SUSPENDED/DISCONNECTED 并进入重试循环，在此循环中，将定期重试连接。 在重新建立连接后，将继续处理。  
  
 其他类型的连接错误不是暂时的（例如，错误的凭据、权限不足以及错误的数据库地址）。 在发生这些错误时，Oracle CDC 服务状态将设置为 ERROR/MISCONFIGURED 或 ERROR/PASSWORD-REQUIRED，并且该服务将被禁用。 在用户修复基础错误后，应手动重新启用 Oracle CDC 实例以便继续处理。  
  
 如果不清楚错误是否是暂时的，则最好将其视为暂时的。  
  
### <a name="handling-target-sql-server-connection-errors"></a>处理目标 SQL Server 连接错误  
 Oracle CDC 服务需要与目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的持久连接。 此连接用于：  
  
-   确保目前没有同名称的其他服务正在使用此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
-   检查启用或禁用了哪一 Oracle CDC 实例并且开始（或停止）其子进程。  
  
 在服务建立与目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接并且确认它是按此名称正在工作的唯一 Oracle CDC 服务后，可检查启用了哪些 Oracle CDC 实例并且开始其处理进程（之后，该服务将在禁用这些进程后停止它们）。 Oracle CDC 实例使用其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接来处理 Oracle CDC 实例的 CDC 数据库。  
  
 在与目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接失败时如何处理错误取决于这些错误是否是暂时的。  
  
 对于已知的非暂时错误（例如错误的凭据、权限不足、错误的连接信息），该服务会将错误记录到 Windows 事件日志并停止运行（该服务无法写入跟踪表，因为它无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）。 在此情况下，用户必须解决该错误，然后重新启动 Oracle CDC Windows 服务。  
  
 对于临时错误和意外错误，将重试几次该操作，并且如果在较长的一段时间中仍继续失败，则该 CDC 服务将停止其 CDC 实例子进程并且返回其初始连接重试（在此时，其他计算机上的 Oracle CDC 服务可能已控制该命名 CDC 服务）。  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>处理目标 SQL Server 存储已满错误  
 在 Oracle CDC 服务检测到它无法将新的更改数据插入目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 数据库后，它会将警告写入事件日志并且尝试插入跟踪记录（尽管出于同样原因可能失败）。 然后，它将按照特定的间隔重试操作，直到操作成功。  
  
### <a name="handling-oracle-cdc-errors"></a>处理 Oracle CDC 错误  
 Oracle CDC 实例读取 Oracle 事务日志并对其进行处理。 如果 CDC 处理遇到错误，则会在 **cdc.xdbcdc_state** 表中报告该错误，并且用户需要基于所报告的错误手动进行干预。  
  
 例如，Oracle CDC 实例可能在延长的时间段中未处于活动状态，并且所需 Oracle 事务日志文件不再可用。 在此情况下，Oracle DBA 必须还原 Oracle CDC 实例的所需日志以便继续处理。  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>处理意外的 Oracle CDC 实例失败  
 Oracle CDC 服务监视其 CDC 实例子进程。 在某一 CDC 实例子进程中止后，CDC 服务将在 MSXDBCDC.dbo.xdbcdc_databases 表中禁用该子进程，并且将其 cdc.xdbcdc_state 状态更新为 ABORTED。 在此情况下，将使用标准的 Windows 错误报告对话框来报告此错误，以便进一步进行分析。  
  
## <a name="see-also"></a>请参阅  
 [Change Data Capture Designer for Oracle by Attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC 实例](the-oracle-cdc-instance.md)  
