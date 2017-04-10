---
title: "在 SSIS 服务器上启用包执行的日志记录 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# 在 SSIS 服务器上启用包执行的日志记录
  本主题介绍在运行已经部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的包时，如何设置或更改该包的日志记录级别。 在运行包时设置的日志记录级别将覆盖你在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中设计时配置的包日志记录。 有关详细信息，请参阅[在 SQL Server Data Tools 中启用包日志记录](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)。  
  
 在 SQL Server“服务器属性”中，“服务器日志记录级别”属性下，可以选择默认服务器范围内的日志记录级别。 可以从本主题中介绍的内置日志记录中选择一项，或者选择现有的自定义日志记录级别。 默认情况下，所选的日志记录级别适用于部署到 SSIS 目录的所有包。 同时也默认适用于运行 SSIS 包的 SQL 代理作业步骤。  
  
 此外，也可使用下列方法之一对单个包指定日志记录级别。 本主题涵盖第一种方法。  
  
-   通过使用“执行包”对话框配置包执行的实例  
  
-   通过使用 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)设置执行实例的参数  
  
-   通过使用“新建作业步骤”对话框配置包执行的 SQL Server 代理作业。  
  
## 通过使用“执行包”对话框设置包的日志记录级别  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，导航到对象资源管理器中的包。  
  
2.  右键单击包，然后选择“执行”。  
  
3.  在 **“执行包”** 对话框中，选择 **“高级”** 选项卡。  
  
4.  在 **“日志记录级别”**下，选择日志记录级别。 本主题包含可用值的说明。  
  
5.  完成所有其他包配置，然后单击 **“确定”** 运行该包。  
  
## 选择日志记录级别  
 以下内置日志记录级别可用。 还可以选择现有的自定义日志记录级别。 本主题包含自定义日志记录级别的说明。  
  
|“日志记录级别”|Description|  
|-------------------|-----------------|  
|InclusionThresholdSetting|关闭日志记录。 仅记录包执行状态。|  
|基本|除了自定义事件和诊断事件之外，记录其余所有事件。 这是默认值。|  
|运行时沿袭|收集跟踪数据流中的沿袭信息所需的数据。 可以分析此沿袭信息以映射任务之间的沿袭关系。 使用此信息，ISV 和开发人员可以构建自定义沿袭映射工具。|  
|性能|仅记录性能统计信息、OnError 和 OnWarning 事件。<br /><br /> **“执行性能”** 报表显示包数据流组件的活动时间和总时间。 仅当上次包执行的日志记录级别设置为 **“性能”** 或 **“详细”**时，此信息才可用。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) 视图显示数据流组件在执行的每个阶段的开始时间和结束时间。 仅当包执行的日志记录级别设置为 **“性能”** 或 **“详细”**时，此视图才会为这些组件显示以上信息。|  
|“详细”|记录所有事件，包括自定义事件和诊断事件。<br /><br /> 自定义事件包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 任务记录的那些事件。 有关自定义事件的详细信息，请参阅 [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md)。<br /><br /> 诊断事件的一个例子就是“DiagnosticEx”  事件。 每当执行包任务执行子包时，此事件均将捕获传递给子包的参数值。<br /><br /> “DiagnosticEx”事件还有助于获取其中出现行级错误的列的名称。 此事件将数据流沿袭映射写入到日志中。 然后就可以使用由错误输出捕获的列标识符来查找此沿袭映射中的列名称。  有关详细信息，请参阅 [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md)。<br /><br /> **DiagnosticEx** 的消息列的值是 XML 文本。 若要查看包执行的消息文本，请查询 [catalog.operation_messages（SSISDB 数据库）](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)视图。 请注意，为了缩减日志大小， **DiagnosticEx** 事件不在其 XML 输出中保留空白。 若要提高可读性，请将日志复制到支持 XML 格式和语法突出显示的 XML 编辑器中 - 例如 Visual Studio 中的 XML 编辑器。<br /><br /> 每当数据流组件向下游组件发送数据时，[catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) 视图就会显示一行。 日志记录级别必须设置为 **“详细”** ，才能在该视图中捕获此信息。|  
  
## 使用“自定义日志记录级别管理”对话框来创建和管理自定义日志记录级别  
 可以创建只收集想要的统计信息和事件的自定义日志记录级别。 还可以选择捕获事件上下文，包括变量值、连接字符串和组件属性。 运行包时，可在任何可以选择内置日志记录级别的位置处，选择自定义日志记录级别。  
  
> [!TIP]  
>  若要捕获包变量的值，必须将该变量的 **IncludeInDebugDump** 属性设置为 **True**。  
  
1.  要创建和管理自定义日志记录级别，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击 SSISDB 数据库并选择“自定义日志记录级别”以打开“自定义日志记录级别管理”对话框。 “自定义日志记录级别”  列表包含所有现有的自定义日志记录级别。  
  
2.  要 **创建** 新的自定义日志记录级别，请单击“创建” ，然后提供名称和描述。 在“统计信息”  和“事件”  选项卡上，选择想要收集的统计信息和事件。 在“事件”  选项卡上，可以选择对单个事件选择“包括上下文”  。 然后单击“保存” 。  
  
3.  要 **更新** 现有的自定义日志记录级别，请在列表中选中并重新配置它，然后单击“保存” 。  
  
4.  要 **删除** 现有的自定义日志记录级别，请在列表中选中它，然后单击“删除” 。  
  
 **自定义日志记录级别的权限。**  
  
-   SSISDB 数据库的所有用户都可以查看自定义日志记录级别，并可在运行包时选择一个自定义日志记录级别。  
  
-   只有 ssis_admin 或 sysadmin 角色中的用户可以创建、更新或删除自定义日志记录级别。  
  
## 另请参阅  
 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)   
 [在 SQL Server Data Tools 中启用包日志记录](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  