---
title: "管理 CDC 实例 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b61e0362a4b29f1721a08469f8df529861e10174
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="manage-a-cdc-instance"></a>管理 CDC 实例
  您可以使用 CDC 设计器控制台查看与您创建的实例有关的信息，以及管理实例操作。  
  
 在左侧窗格中单击某一实例的名称可查看与该实例有关的信息。  
  
> [!NOTE]  
>  如果您在左侧窗格中选择某一服务，则可用实例的列表也会显示在 CDC 设计器控制台的中央。 如果您在该部分中选择某一实例，则可以在右侧窗格中执行任务；但是，您将不能在属性选项卡中查看信息。  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>在显示 CDC 实例信息时您可以执行的操作  
 从右窗格中执行以下操作：  
  
 **开始**  
 单击“开始”可为所选的 CDC 实例开始捕获更改。  
  
 **停止**  
 单击“停止”可为所选的 CDC 实例停止捕获更改。 在您停止该 CDC 实例时，在该时间点前已捕获的更改将不会丢失，并且这些更改将在恢复该 CDC 实例时提供。  
  
 **重置**  
 单击“重置”可将 CDC 实例重置为其初始（空）状态。 此选项在 CDC 实例停止后可用。 更改表中的所有更改以及 CDC 实例内部状态将被删除。 当 CDC 实例在以后启动时，变更捕获将从该时间点开始，并且仅包含在 CDC 实例启动后开始的事务。  
  
 在确认对话框中单击 **“确定”** ，以便确认您要重置 CDC 实例并且删除写入更改表的更改。  
  
 **删除**  
 单击“删除”可永久删除 CDC 实例。 此选项仅在 CDC 实例停止后可用。  
  
 在确认对话框中单击 **“确定”** ，以便确认您要删除 CDC 实例。  
  
 **Oracle 日志记录脚本**  
 单击此链接将显示具有 Oracle 补充日志记录脚本的“Oracle 日志记录脚本”对话框。 有关可以在此对话框中执行的操作的信息，请参阅 [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md)。  
  
> [!NOTE]  
>  在您运行补充日志记录脚本时，“用于运行脚本的 Oracle 凭据”对话框将打开，您可以在其中提供有效的 Oracle 用户名和密码。 有关如何提供适当的 Oracle 凭据的信息，请参阅 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)。  
  
 **CDC 实例部署脚本**  
 单击此链接可显示 CDC 实例部署脚本的“CDC 实例部署脚本”对话框。 有关此对话框的信息，请参阅 [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md)。  
  
 **属性**  
 单击此链接可打开属性编辑器。 您使用属性编辑器编辑 CDC 实例配置。 有关编辑 CDC 实例属性的详细信息，请参阅 [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md)。  
  
 **查看器的选项卡**  
  
 在您查看 CDC 实例的信息时，以下查看器选项卡可用。 这些选项卡中的信息是只读的。  
  
 **“状态”**  
 此选项卡提供有关 CDC 实例的当前状态的信息和统计信息。 其中包含以下信息。  
  
-   **状态**：一个指示 CDC 实例的当前状态的图标。 下面将介绍这些状态。  
  
    |||  
    |-|-|  
    |![错误](../../integration-services/change-data-capture/media/error.gif "错误")|**错误**。 Oracle CDC 实例因为发生了不可重试的错误而未运行。 以下子状态可用：<br /><br /> **配置不当**：发生了需要手动干预的配置错误。<br /><br /> **要求提供密码**：没有为 Oracle CDC 实例设置密码或密码无效。<br /><br /> **意外**。 所有其他不可恢复错误。|  
    |![正常](../../integration-services/change-data-capture/media/okay.gif "Okay")|**正在运行**：CDC 实例正在运行并且正在处理更改记录。 以下子状态可用：<br /><br /> **空闲**：所有更改记录都已处理并且存储在目标更改表中。 没有活动事务。<br /><br /> **正在处理**：存在正处理、但尚未写入更改表的更改记录。|  
    |![停止](../../integration-services/change-data-capture/media/stop.gif "停止")|**已停止**：CDC 实例未在运行。 该已停止状态指示 CDC 实例已正常停止。|  
    |![已暂停](../../integration-services/change-data-capture/media/paused.gif "已暂停")|**已暂停**：CDC 实例正在运行，但由于可重试错误处理已挂起。 以下子状态可用：<br /><br /> **断开连接**：无法建立到源 Oracle 数据库的连接。 在连接恢复时会继续处理。<br /><br /> **存储**：存储已满。 在其他存储变为可用时将继续处理。<br /><br /> **记录器**：记录器连接到 Oracle，但由于临时问题（例如，所需的事务日志不可用）无法读取 Oracle 事务日志。|  
  
-   **详细状态**：当前子状态。  
  
-   **状态消息**：有关当前状态的详细信息。  
  
-   **时间戳**：上次从状态表中读取 CDC 状态时的 UTC 时间。  
  
-   **当前正处理**：您在此部分中监视下列信息。  
  
    -   **上一个事务时间戳**：写入更改表的上一个事务的本地时间。  
  
    -   **上一个更改时间戳**：Oracle CDC 实例在源 Oracle 数据库事务日志中看到的最近更改的本地时间。 它提供了读取 Oracle 事务日志时与 CDC 实例的当前延迟有关的信息。  
  
    -   **事务日志头 CN**：从 Oracle 事务日志读取的最近更改号 (CN)。  
  
    -   **事务日志尾 CN**：用于恢复或重新启动 CDC 实例的更改号。 在发生重新启动或任何其他类型的失败（包括群集故障转移）时 Oracle CDC 实例将重新定位到此位置。  
  
    -   **当前 CN**：在源 Oracle 数据库（而非事务日志）中看到的最后的更改号 (SCN)。  
  
    -   **活动事务**：Oracle CDC 实例正在处理但尚未决定（提交/回退）的源 Oracle 事务的当前数目。  
  
    -   **暂存事务**：暂存到 [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) 表的当前源 Oracle 事务的数目。  
  
-   **计数器**：您在此部分中监视下列信息。  
  
    -   **完成的事务数**：自上次重置 CDC 实例后完成的事务数。 此计数中不包括那些不包含有关表的事务。  
  
    -   **写入的更改数**：已写入 SQL Server 更改表的更改的数目。  
  
 **Oracle**  
 显示与 CDC 实例及其与 Oracle 数据库的连接有关的信息。 此选项卡为只读。 若要编辑这些属性，请在左侧窗格中右键单击实例，然后选择“属性”；或者在右侧窗格中单击“属性”以打开“\<实例> 属性”对话框。  
  
 有关这些属性以及如何编辑它们的信息，请参阅 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)。  
  
 **表**  
 显示有关 CDC 实例中包含的表的信息。 在此处也提供列信息。 此选项卡为只读。 若要编辑这些属性，请在左侧窗格中右键单击实例，然后选择“属性”；或者在右侧窗格中单击“属性”以打开“\<实例> 属性”对话框。  
  
 有关这些属性以及如何编辑它们的信息，请参阅 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)。  
  
 **高级**  
 显示 CDC 实例的高级属性和属性值。 此选项卡为只读。 若要编辑这些属性，请在左侧窗格中右键单击实例，然后选择“属性”；或者在右侧窗格中单击“属性”以打开“\<实例> 属性”对话框。  
  
 有关这些属性以及如何编辑它们的信息，请参阅 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何创建 SQL Server 更改数据库实例](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [如何查看 CDC 实例属性](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [如何编辑 CDC 实例属性](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [使用新建实例向导](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
