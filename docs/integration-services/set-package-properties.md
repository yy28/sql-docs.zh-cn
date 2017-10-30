---
title: "设置包属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 658f7e77fe821fa4821b61162662175ab5f840c1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="set-package-properties"></a>设置包属性
  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供的图形界面创建包时，可以在“属性”窗口中设置包对象的各个属性。  
  
 **“属性”** 窗口按分类和字母顺序排序列出了一系列属性列表。 若要按类别排列 **“属性”** 窗口，请单击“按分类顺序”图标。  
  
 按类别排列时， **“属性”** 窗口将属性分成以下类别：  
  
-   [检查点](#Checkpoints)  
  
-   [执行](#Execution)  
  
-   [强制执行值](#ForcedExecutionValue)  
  
-   [标识](#Identification)  
  
-   [杂项](#Misc)  
  
-   [Security](#Security)  
  
-   [中的](#Transactions)  
  
-   [版本](#Version)  
  
 有关不能在中设置的其他包属性**属性**窗口中，请参阅<xref:Microsoft.SqlServer.Dts.Runtime.Package>。  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>在“属性”窗口中设置包属性  
  
-   [设置包的属性](http://msdn.microsoft.com/library/0d20346e-475c-412f-b3ff-7bce25242b7a)  
  
## <a name="properties-by-category"></a>按类别排列的属性  
 下表列出了按类别排列的包属性。  
  
###  <a name="Checkpoints"></a> 检查点  
 使用此类别中的属性可以从包控制流中的某一故障点重新启动包，而不是从包控制流的开始处重新运行包。 有关详细信息，请参阅 [Restart Packages by Using Checkpoints](../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
|属性|Description|  
|--------------|-----------------|  
|**CheckpointFileName**|用于捕获使包重新启动的检查点信息的文件的名称。 当包成功完成时，该文件便会被删除。|  
|**CheckpointUsage**|指定何时可以重新启动包。 具体的值为 **Never**、 **IfExists**和 **Always**。 此属性的默认值为 **Never**，指示包不能重新启动。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>。|  
|**SaveCheckpoints**|指定在包运行时，是否将检查点写入检查点文件。 此属性的默认值为 **False**。|  
  
> [!NOTE]  
>  dtexec 的 **/CheckPointing on** 选项等效于将包的 **SaveCheckpoints** 属性设置为 True，并将 **CheckpointUsage** 属性设置为“Always”。 有关详细信息，请参阅 [dtexec Utility](../integration-services/packages/dtexec-utility.md)。  
  
###  <a name="Execution"></a> 执行  
 此类别中的属性可配置包对象的运行时行为。  
  
|属性|Description|  
|--------------|-----------------|  
|**DelayValidation**|指示是否将包验证推迟至包运行之时进行。 此属性的默认值为 **False**。|  
|**Disable**|指示包是否已禁用。 此属性的默认值为 **False**。|  
|**DisableEventHandlers**|指定包事件处理程序是否运行。 此属性的默认值为 **False**。|  
|**FailPackageOnFailure**|指定如果包组件中出现错误时，包是否失败。 此属性的唯一有效值为 **False**。|  
|**FailParentOnError**|指定如果子容器中出现错误，父容器是否失败。 该属性的默认值为 **False**。|  
|**MaxConcurrentExecutables**|包可以同时执行的可执行文件数目。 此属性的默认值为 **-1**，表示没有任何限制。|  
|**MaximumErrorCount**|包停止运行前可以出现的最大错误数。 此属性的默认值为 **1**。|  
|**PackagePriorityClass**|包线程的 Win32 线程优先级类。 其值分别为 **Default**、 **AboveNormal**、 **Normal**、 **BelowNormal**、 **Idle**。 此属性的默认值为 **Default**。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>。|  
  
###  <a name="ForcedExecutionValue"></a> 强制执行值  
 此类别中的属性用于配置包的可选执行值。  
  
|属性|Description|  
|--------------|-----------------|  
|**ForcedExecutionValue**|如果 ForceExecutionValue 设置为 **True**，则为用于指定包返回的可选执行值的值。 此属性的默认值为 **0**。|  
|**ForcedExecutionValueType**|ForcedExecutionValue 的数据类型。 此属性的默认值为 **Int32**。|  
|**ForceExecutionValue**|指定容器的可选执行值是否应强制包含特定值的布尔值。 此属性的默认值为 **False**。|  
  
###  <a name="Identification"></a> 标识  
 此类别中的属性提供诸如包的唯一标识符和名称等信息。  
  
|属性|Description|  
|--------------|-----------------|  
|**CreationDate**|包的创建日期。|  
|**CreatorComputerName**|创建包的计算机的名称。|  
|**CreatorName**|包创建者的姓名。|  
|**Description**|包功能说明。|  
|**ID**|包 GUID，该属性是在创建包时分配的。 该属性为只读。 若要生成新的随机值**ID**属性中，选择**\<生成新的 ID\>** 下拉列表中。|  
|**名称**|包的名称。|  
|**PackageType**|包类型。 其值为： **Default**、 **DTSDesigner**、 **DTSDesigner100**、 **DTSWizard**、 **SQLDBMaint**和 **SQLReplication**。 此属性的默认值为 **Default**。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>。|  
  
###  <a name="Misc"></a> 杂项  
 此类别中的属性用于访问包所使用的配置和表达式，以及提供有关包的区域设置和日志记录模式的信息。 有关详细信息，请参阅 [在包中使用属性表达式](../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
|属性|Description|  
|--------------|-----------------|  
|**配置**|包使用的配置集合。 单击浏览按钮 **(…)** 可以查看和配置包配置。|  
|**表达式**|单击浏览按钮 **(…)** 可以为包属性创建表达式。<br /><br /> 请注意，你可以为对象模型包含的所有包属性（而不仅仅是“属性”窗口中列出的属性）创建属性表达式。<br /><br /> 有关详细信息，请参阅 [在包中使用属性表达式](../integration-services/expressions/use-property-expressions-in-packages.md)。<br /><br /> 若要查看现有的属性表达式，请展开 **Expressions**。 单击表达式文本框中的浏览按钮 **(…)** 可以修改和计算表达式。|  
|**ForceExecutionResult**|包的执行结果。 其值为： **None**、 **Success**、 **Failure**和 **Completion**。 此属性的默认值为 **None**。 有关详细信息，请参阅 T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult。|  
|**LocaleId**|Microsoft Win32 区域设置。 此属性的默认值为本地计算机上操作系统的区域设置。|  
|**LoggingMode**|指定包日志记录行为的值。 具体的值为 **Disabled**、 **Enabled**和 **UseParentSetting**。 此属性的默认值为 **UseParentSetting**。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>。|  
|**OfflineMode**|指示该包是否处于脱机模式下。 该属性为只读。 该属性在项目级设置。 通常， [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器将尝试连接包使用的每个数据源以验证与源和目标相关联的元数据。 您可以从 **“SSIS”** 菜单中启用 **“脱机工作”** （即使在打开包之前也可以）以阻止这些连接尝试和数据源不可用时导致的验证错误。 您还可以启用 **“脱机工作”** 以加快设计器中操作的速度，而仅在需要验证包的时候再禁用此选项。|  
|**SuppressConfigurationWarnings**|指示是否取消配置生成的警告。 此属性的默认值为 **False**。|  
|**UpdateObjects**|指示当包所含对象的更新版本可用时，是否更新包以使用更新版本的对象。 例如，如果此属性设置为 **True**，则会更新包含大容量插入任务的包，以使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的更新版本的大容量插入任务。 此属性的默认值为 **False**。|  
  
###  <a name="Security"></a> Security  
 此类别中的属性用于设置包的保护级别。 有关详细信息，请参阅 [Access Control for Sensitive Data in Packages](../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
|属性|Description|  
|--------------|-----------------|  
|**PackagePassword**|需要密码的包保护级别 (**EncryptSensitiveWithPassword** 和 **EncryptAllWithPassword**) 的密码。|  
|**ProtectionLevel**|包的保护级别。 其值为： **DontSaveSensitive**、 **EncryptSensitiveWithUserKey**、 **EncryptSensitiveWithPassword**、 **EncryptAllWithPassword**和 **ServerStorage**。 此属性的默认值为 **EncryptSensitiveWithUserKey**。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>。|  
  
###  <a name="Transactions"></a> 中的  
 此类别中的属性用于配置包的隔离级别和事务选项。 有关详细信息，请参阅 [Integration Services 事务](../integration-services/integration-services-transactions.md)。  
  
|属性|Description|  
|--------------|-----------------|  
|**IsolationLevel**|包事务的隔离级别。 其值为： **Unspecified**、 **Chaos**、 **ReadUncommitted**、 **ReadCommitted**、 **RepeatableRead**、 **Serializable**和 **Snapshot**。 此属性的默认值为 **Serializable**。<br /><br /> 注意： **IsolationLevel** 属性的 **Snapshot** 值与包事务不兼容。 因此，您无法使用 **IsolationLevel** 属性将包事务的隔离级别设为 **Shapshot**。 而是使用 SQL 查询将包事务设为 **Snapshot**。 有关详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。<br /><br /> 仅当 **IsolationLevel** 属性的值设为 **TransactionOption** 时，系统才将 **Required**属性应用到包事务。<br /><br /> 在以下条件成立时，将忽略子容器请求的 **IsolationLevel** 属性的值：<br />子容器的 **TransactionOption** 属性的值为 **Supported**。<br />子容器联接父容器的事务。<br /><br /> 只有在容器开始新的事务时，才遵从该容器请求的 **IsolationLevel** 属性的值。 在以下条件成立时，容器将开始新的事务：<br />容器的 **TransactionOption** 属性的值为 **Required**。<br />父容器尚未启动事务。<br /><br /> <br /><br /> 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>。|  
|**TransactionOption**|包的事务参与情况。 其值为： **NotSupported**、 **Supported**、 **Required**。 此属性的默认值为 **Supported**。 有关详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>。|  
  
###  <a name="Version"></a> 版本  
 此类别中的属性用于提供包对象的版本信息。  
  
|属性|Description|  
|--------------|-----------------|  
|**VersionBuild**|包的内部版本号。|  
|**VersionComments**|包的版本注释。|  
|**VersionGUID**|包版本的 GUID。 该属性为只读。|  
|**VersionMajor**|包的最新主版本。|  
|**VersionMinor**|包的最新次版本。|  

## <a name="set-package-properties-in-the-properties-window"></a>在属性窗口中设置包属性 
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要配置的包所在的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中双击此包，将其在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开，或者右键单击并选择“视图设计器”。  
  
3.  单击 **“控制流”** 选项卡，然后执行下列操作之一：  
  
    -   右键单击控制流设计图面背景中的任意位置，然后单击“属性”。  
  
    -   在 **“视图”** 菜单上，单击 **“属性窗口”**。  
  
4.  在 **“属性”** 窗口中编辑包属性。  
  
5.  在 **“文件”** 菜单上单击 **“保存选定项”** ，保存已更新的包。  
  

