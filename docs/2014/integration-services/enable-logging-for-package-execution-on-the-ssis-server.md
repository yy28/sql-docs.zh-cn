---
title: 在 SSIS 服务器上启用包执行的日志记录 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47f74d4510b46b984eb58706ff4ac159cb8b1352
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059371"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>在 SSIS 服务器上启用包执行的日志记录
  本过程介绍在执行已经部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器的包时，如何设置或更改该包的日志记录级别。 在执行包时设置的日志记录级别优先于使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 配置的包日志记录。 有关详细信息，请参阅 [在 SQL Server Data Tools 中启用包日志记录](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) 。  
  
 可使用下列方法之一指定日志记录级别。 本主题涵盖第一种方法。  
  
-   通过使用“执行包”对话框配置包执行的实例  
  
-   通过使用 [catalog.set_execution_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)设置执行实例的参数  
  
-   通过使用“新建作业步骤”对话框配置包执行的 SQL Server 代理作业。  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>通过使用“执行包”对话框设置包的日志记录级别  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，导航到对象资源管理器中的包。  
  
2.  右键单击包，然后选择“执行”。****  
  
3.  在 **“执行包”** 对话框中，选择 **“高级”** 选项卡。  
  
4.  在 **“日志记录级别”** 下，选择日志记录级别。 有关可用值的说明，请参阅下表。  
  
5.  完成所有其他包配置，然后单击 **“确定”** 运行该包。  
  
 以下日志记录级别可用。  
  
|“日志记录级别”|说明|  
|-------------------|-----------------|  
|无|关闭日志记录。 仅记录包执行状态。|  
|基本|除了自定义事件和诊断事件之外，记录其余所有事件。 这是默认值。|  
|性能|仅记录性能统计信息、OnError 和 OnWarning 事件。<br /><br /> **“执行性能”** 报表显示包数据流组件的活动时间和总时间。 仅当上次包执行的日志记录级别设置为 **“性能”** 或 **“详细”** 时，此信息才可用。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)。<br /><br /> [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) 视图显示数据流组件在执行的每个阶段的开始时间和结束时间。 仅当包执行的日志记录级别设置为 **“性能”** 或 **“详细”** 时，此视图才会为这些组件显示以上信息。|  
|“详细”|记录所有事件，包括自定义事件和诊断事件。<br /><br /> 诊断事件的一个例子就是 DiagnosticEx 事件。 每当执行包任务执行子包时，都会记录此事件。 事件消息包含传递给子包的参数值<br /><br /> DiagnosticEx 的消息列的值是 XML 文本。 . 若要查看包执行的消息文本，请查询 [catalog.operation_messages（SSISDB 数据库）](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)视图。<br /><br /> 注意：自定义事件包括[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]任务记录的那些事件。 有关详细信息，请参阅[日志记录的自定义消息](../../2014/integration-services/custom-messages-for-logging.md)。<br /><br /> 每当数据流组件向下游组件发送数据时， [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) 视图就会显示一行。 日志记录级别必须设置为 **“详细”** ，才能在该视图中捕获此信息。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS&#41; 日志记录](performance/integration-services-ssis-logging.md)   
 [在 SQL Server Data Tools 中启用包日志记录](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
