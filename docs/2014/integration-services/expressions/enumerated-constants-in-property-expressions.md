---
title: 属性表达式中的枚举常量 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b22e25ad9053ed4da0187035cff00ff7e3ca70af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898895"
---
# <a name="enumerated-constants-in-property-expressions"></a>属性表达式中的枚举常量
  如果属性表达式包括枚举器成员列表中的值，则该表达式必须使用枚举器成员的数值，而不是成员的友好名称。 例如，如果表达式设置 `LoggingMode` 属性，则必须使用数值 2 而不是友好名称“Disabled”。  
  
 此主题只列出通常会在属性表达式中使用其成员的枚举器的友好名称的等价数值。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型包括很多其他枚举器，在编写对象模型以便以编程方式生成包时，或为任务和数据流组件等自定义包元素编写代码时，需要使用这些枚举器。  
  
 除了包和包对象的自定义属性外， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“属性”窗口还包括一组可用于包、任务以及 Foreach 循环、For 循环和序列容器的属性。 从枚举器的设置的值的常见属性`ForceExecutionResult`， `LoggingMode`， `IsolationLevel`，和`Transaction Option`的通用属性部分中列出。  
  
 以下部分提供了有关枚举常量的信息：  
  
 [“包”](#Package)  
  
 [Foreach 循环枚举器](#Foreach)  
  
 [“任务”](#Tasks)  
  
 [维护计划任务](#MaintenancePlanTasks)  
  
 [通用属性](#CommonProperties)  
  
##  <a name="Package"></a> “包”  
 下表列出了通过使用枚举器中的值所设置的包的属性的友好名称和等价数值。  
  
 `PackageType` 通过使用中的值的属性集`DTSPackageType`枚举。  
  
|DTSPackageType 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|默认|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage` 通过使用中的值的属性集`DTSCheckpointUsage`枚举。  
  
|DTSCheckpointUsage 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|从不|0|  
|IfExists|1|  
|始终|2|  
  
 `PackagePriorityClass` 通过使用中的值的属性集`DTSPriorityClass`枚举。  
  
|DTSPriorityClass 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|默认|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel` 通过使用中的值的属性集`DTSProtectionLevel`枚举。  
  
|DTSProtectionLevel 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> 优先约束  
 `EvalOp` 通过使用中的值的属性集`DTSPrecedenceEvalOp`枚举。  
  
|DTSPrecedenceEvalOp 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|表达式|1|  
|约束|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value` 通过使用中的值的属性集`DTSExecResult`枚举。  
  
|友好名称|数值|  
|-------------------|-------------------|  
|成功|0|  
|失败|1|  
|Completion|2|  
|已取消|3|  
  
##  <a name="Foreach"></a> Foreach 循环枚举器  
 Foreach 循环包括一组其属性可以由属性表达式设置的枚举器。  
  
### <a name="foreach-ado-enumerator"></a>Foreach ADO 枚举器  
 `Type` 通过使用中的值的属性集`ADOEnumerationType`枚举。  
  
|ADOEnumerationType 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Foreach Nodelist 枚举器  
 `SourceDocumentType``InnerXPathStringSourceType`，并**OuterXPathStringSourceType**通过使用中的值的属性集`SourceType`枚举。  
  
|SourceType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|文件连接|0|  
|变量|1|  
|DirectInput|2|  
  
 `EnumerationType` 通过使用中的值的属性集`EnumerationType`枚举。  
  
|EnumerationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|节点|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType` 通过使用中的值的属性集`InnerElementType`枚举。  
  
|InnerElementType 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|节点|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> “任务”  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括许多其属性可以由属性表达式设置的任务。  
  
### <a name="analysis-services-execute-ddl-task"></a>Analysis Services 执行 DDL 任务  
 `SourceType` 通过使用中的值的属性集`DDLSourceType`枚举。  
  
|DDLSourceType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|文件连接|1|  
|变量|2|  
  
### <a name="bulk-insert-task"></a>大容量插入任务  
 `DataFileType` 通过使用中的值的属性集`DTSBulkInsert_DataFileType`枚举。  
  
|DTSBulkInsert_DataFileType 中的友好名称|数值|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>执行 SQL 任务  
 `ResultSetType` 通过使用中的值的属性集`ResultSetType`枚举。  
  
|ResultSetType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType` 通过使用中的值的属性集`SqlStatementSourceType`枚举。  
  
|SqlStatementSourceType 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|文件连接|2|  
|变量|3|  
  
### <a name="file-system-task"></a>文件系统任务  
 `Operation` 通过使用中的值的属性集`DTSFileSystemOperation`枚举。  
  
|DTSFileSystemOperation 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 `Attributes` 通过使用中的值的属性集`DTSFileSystemAttributes`枚举。  
  
|DTSFileSystemAttributes 中的友好名称|数值|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|ReadOnly|4|  
|系统|8|  
  
### <a name="ftp-task"></a>FTP 任务  
 `Operation` 通过使用中的值的属性集`DTSFTPOp`枚举。  
  
|DTSFTPOp 中的友好名称|数值|  
|-------------------------------|-------------------|  
|Send|0|  
|Receive|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType` 通过使用中的值的属性集`MQMessageType`枚举。  
  
|MQMessageType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType` 通过使用中的值的属性集`MQStringMessageCompare`枚举。  
  
|MQStringMessageCompare 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType` 通过使用中的值的属性集`MQType`枚举。  
  
|MQType 中的友好名称|数值|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>发送邮件任务  
 `MessageSourceType` 通过使用中的值的属性集`SendMailMessageSourceType`枚举。  
  
|SendMailMessageSourceType 中的友好名称|数值|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|文件连接|1|  
|变量|2|  
  
 `Priority` 通过使用中的值的属性集`MailPriority`枚举。  
  
|MailPriority 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|High|1|  
|Normal|3|  
|Low|5|  
  
### <a name="transfer-database-task"></a>传输数据库任务  
 `Action` 通过使用中的值的属性集`TransferAction`枚举。  
  
|TransferAction 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|复制|0|  
|“移动”|1|  
  
 `Method` 通过使用中的值的属性集`TransferMethod`枚举。  
  
|TransferMethod 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>传输错误消息任务  
 `IfObjectExists` 通过使用中的值的属性集`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>传输作业任务  
 `IfObjectExists` 通过使用中的值的属性集`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>传输登录名任务  
 `IfObjectExists` 通过使用中的值的属性集`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 `LoginsToTransfer` 通过使用中的值的属性集`LoginsToTransfer`枚举。  
  
|LoginsToTransfer 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>传输主存储过程任务  
 `IfObjectExists` 通过使用中的值的属性集`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>传输 SQL Server 对象任务  
 `ExistingData` 通过使用中的值的属性集`ExistingData`枚举。  
  
|ExistingData 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|替换|0|  
|追加|1|  
  
### <a name="web-service-task"></a>Web 服务任务  
 `OutputType` 通过使用中的值的属性集`DTSOutputType`枚举。  
  
|DTSOutputType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|文件|0|  
|变量|1|  
  
### <a name="wmi-data-reader-task"></a>WMI 数据读取器任务  
 `OverwriteDestination` 通过使用中的值的属性集`OverwriteDestination`枚举。  
  
|OverwriteDestination 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 `OutputType` 通过使用中的值的属性集`OutputType`枚举。  
  
|OutputType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 `DestinationType` 通过使用中的值的属性集`DestinationType`枚举。  
  
|DestinationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|变量|1|  
  
 `WqlQuerySourceType` 通过使用中的值的属性集`QuerySourceType`枚举。  
  
|QuerySourceType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|DirectInput|1|  
|变量|2|  
  
 WMI 事件观察器`ActionAtEvent`通过使用中的值的属性集`ActionAtEvent`枚举。  
  
|ActionAtEvent 中的友好名称|数值|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 `ActionAtTimeout` 通过使用中的值的属性集`ActionAtTimeout`枚举。  
  
|ActionAtTimeout 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 `AfterEvent` 通过使用中的值的属性集`AfterEvent`枚举。  
  
|AfterEvent 中的友好名称|数值|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout` 通过使用中的值的属性集`AfterTimeout`枚举。  
  
|AfterTimeout 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType` 通过使用中的值的属性集`QuerySourceType`枚举。  
  
|QuerySourceType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|DirectInput|1|  
|变量|2|  
  
### <a name="xml-task"></a>XML 任务  
 `OperationType` 通过使用中的值的属性集`DTSXMLOperation`枚举。  
  
|DTSXMLOperation 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|验证|0|  
|XSLT|1|  
|XPATH|2|  
|合并|3|  
|差异|4|  
|Patch|5|  
  
 `SourceType``SecondOperandType`，并`XPathSourceType`通过使用中的值的属性集`DTSXMLSourceType`枚举。  
  
|DTSXMLSourceType 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|文件连接|0|  
|变量|1|  
|DirectInput|2|  
  
 `DestinationType` 并**DiffGramDestinationType**通过使用中的值的属性集`DTSXMLSaveResultTo`枚举。  
  
|DTSXMLSaveResultTo 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|文件连接|0|  
|变量|1|  
  
 `ValidationType` 通过使用中的值的属性集`DTSXMLValidationType`枚举。  
  
|DTSXMLValidationType 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 `XPathOperation` 通过使用中的值的属性集`DTSXMLXPathOperation`枚举。  
  
|DTSXMLXPathOperation 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|值|1|  
|NodeList|2|  
  
 `DiffOptions` 通过使用中的值的属性集`DTSXMLDiffOptions`枚举。 此枚举器中的选项不相互排斥。 若要使用多个选项，请将要应用的选项作为逗号分隔的列表提供。  
  
|DTSXMLDiffOptions 中的友好名称|数值|  
|----------------------------------------|-------------------|  
|None|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm` 通过使用中的值的属性集`DTSXMLDiffAlgorithm`枚举。  
  
|DTSXMLDiffAlgorithm 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Fast|1|  
|Precise|2|  
  
##  <a name="MaintenancePlanTasks"></a> 维护计划任务  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括的一组任务将执行在维护计划和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中使用的 SQL Server 任务。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持通过编程来使用这些任务，而且编程参考文档不包括这些任务及其枚举器的 API 文档。  
  
### <a name="all-maintenance-tasks"></a>所有维护任务  
 所有维护任务均使用以下枚举来设置指定的属性。  
  
 `DatabaseSelectionType` 通过使用中的值的属性集`DatabaseSelection`枚举。  
  
|DatabaseSelection 中的友好名称|数值|  
|----------------------------------------|-------------------|  
|None|0|  
|All|1|  
|系统|2|  
|“用户”|3|  
|Specific|4|  
  
 `TableSelectionType` 通过使用中的值的属性集`TableSelection`枚举。  
  
|TableSelection 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|None|0|  
|All|1|  
|Specific|2|  
  
 `ObjectTypeSelection` 通过使用中的值的属性集`ObjectType`枚举。  
  
|ObjectType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|表|0|  
|“查看”|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>“备份数据库”任务  
 `DestinationCreationType` 通过使用中的值的属性集`DestinationType`枚举。  
  
|DestinationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|1|  
  
 `ExistingBackupsAction` 通过使用中的值的属性集`ActionForExistingBackups`枚举。  
  
|ActionForExistingBackups 中的友好名称|数值|  
|-----------------------------------------------|-------------------|  
|追加|0|  
|Overwrite|1|  
  
 `BackupAction` 通过使用中的值的属性集`BackupTaskType`枚举。 此属性与 `BackupIsIncremental` 属性一起使用以定义该任务所执行的备份的类型。  
  
|BackupTaskType 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|“数据库”|0|  
|文件|1|  
|日志|2|  
  
 `BackupDevice` 通过使用中的值的属性集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理对象 (SMO)`DeviceType`枚举。  
  
|DeviceType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|磁带|1|  
|文件|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>“清除维护”任务  
 `FileTypeSelected` 通过使用中的值的属性集`FileType`枚举。  
  
|FileType 中的友好名称|数值|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 `OlderThanTimeUnitType` 通过使用中的值的属性集`TimeUnitType`枚举。  
  
|TimeUnitType 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|Day|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>“更新统计信息”任务  
 `UpdateType` 通过使用中的值的属性集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理对象 (SMO)`StatisticsTarget`枚举。  
  
|StatisticsTarget 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|“列”|1|  
|索引|2|  
|All|3|  
  
##  <a name="CommonProperties"></a> 通用属性  
 包、任务和 Foreach 循环、For 循环和序列容器可以使用以下枚举来设置指定的属性。  
  
 `ForceExecutionResult` 通过使用中的值的属性集`DTSForcedExecResult`枚举。  
  
|DTSForcedExecResult 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|None|-1|  
|成功|0|  
|失败|1|  
|Completion|2|  
  
 `IsolationLevel` 由.NET Framework 的属性集`IsolationLevel`枚举。 详细信息，请参阅位于 [MSDN Library](https://go.microsoft.com/fwlink?LinkId=17313)中的 .NET Framework 类库。  
  
 `LoggingMode` 通过使用中的值的属性集`DTSLoggingMode`枚举。  
  
|DTSLoggingMode 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|Enabled|1|  
|禁用|2|  
  
 `TransactionOption` 通过使用中的值的属性集`DTSTransactionOption`枚举。  
  
|DTSTransactionOption 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|支持|1|  
|Required|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [添加或更改属性表达式](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>请参阅  
 [在包中使用属性表达式](use-property-expressions-in-packages.md)   
 [Integration Services (SSIS) 包](../integration-services-ssis-packages.md)   
 [Integration Services 容器](../control-flow/integration-services-containers.md)   
 [Integration Services 任务](../control-flow/integration-services-tasks.md)   
 [优先约束](../control-flow/precedence-constraints.md)  
  
  
