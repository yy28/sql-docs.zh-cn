---
title: 属性表达式中的枚举常量 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d000c77263a0448ff838bff42a5020b86a299a72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221827"
---
# <a name="enumerated-constants-in-property-expressions"></a>属性表达式中的枚举常量
  如果属性表达式包括枚举器成员列表中的值，则该表达式必须使用枚举器成员的数值，而不是成员的友好名称。 例如，如果表达式设置`LoggingMode`属性，则必须使用数值 2 而不是友好名称已禁用。  
  
 此主题只列出通常会在属性表达式中使用其成员的枚举器的友好名称的等价数值。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象模型包括很多其他枚举器，在编写对象模型以便以编程方式生成包时，或为任务和数据流组件等自定义包元素编写代码时，需要使用这些枚举器。  
  
 除了包和包对象的自定义属性外， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“属性”窗口还包括一组可用于包、任务以及 Foreach 循环、For 循环和序列容器的属性。 由枚举器中的值所设置的通用属性（`ForceExecutionResult`、`LoggingMode`、`IsolationLevel` 和 `Transaction Option`）将在“通用属性”部分中列出。  
  
 以下部分提供了有关枚举常量的信息：  
  
 [“包”](#Package)  
  
 [Foreach 循环枚举器](#Foreach)  
  
 [“任务”](#Tasks)  
  
 [维护计划任务](#MaintenancePlanTasks)  
  
 [通用属性](#CommonProperties)  
  
##  <a name="Package"></a> “包”  
 下表列出了通过使用枚举器中的值所设置的包的属性的友好名称和等价数值。  
  
 `PackageType` 属性-通过使用中的值设置`DTSPackageType`枚举。  
  
|DTSPackageType 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|，则“默认”|0|  
|DTSWizard|@shouldalert|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage` 属性-通过使用中的值设置`DTSCheckpointUsage`枚举。  
  
|DTSCheckpointUsage 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|从不|0|  
|IfExists|@shouldalert|  
|始终|2|  
  
 `PackagePriorityClass` 属性-通过使用中的值设置`DTSPriorityClass`枚举。  
  
|DTSPriorityClass 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|，则“默认”|0|  
|AboveNormal|@shouldalert|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel` 属性-通过使用中的值设置`DTSProtectionLevel`枚举。  
  
|DTSProtectionLevel 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|@shouldalert|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> 优先约束  
 `EvalOp` 属性-通过使用中的值设置`DTSPrecedenceEvalOp`枚举。  
  
|DTSPrecedenceEvalOp 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|表达式|@shouldalert|  
|约束|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value` 属性-通过使用中的值设置`DTSExecResult`枚举。  
  
|友好名称|数值|  
|-------------------|-------------------|  
|成功|0|  
|失败|@shouldalert|  
|Completion|2|  
|已取消|3|  
  
##  <a name="Foreach"></a> Foreach 循环枚举器  
 Foreach 循环包括一组其属性可以由属性表达式设置的枚举器。  
  
### <a name="foreach-ado-enumerator"></a>Foreach ADO 枚举器  
 `Type` 属性-通过使用中的值设置`ADOEnumerationType`枚举。  
  
|ADOEnumerationType 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|@shouldalert|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Foreach Nodelist 枚举器  
 `SourceDocumentType``InnerXPathStringSourceType`，并**OuterXPathStringSourceType**属性-通过使用中的值设置`SourceType`枚举。  
  
|SourceType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|文件连接|0|  
|变量|@shouldalert|  
|DirectInput|2|  
  
 `EnumerationType` 属性-通过使用中的值设置`EnumerationType`枚举。  
  
|EnumerationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|节点|@shouldalert|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType` 属性-通过使用中的值设置`InnerElementType`枚举。  
  
|InnerElementType 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|节点|@shouldalert|  
|NodeText|2|  
  
##  <a name="Tasks"></a> “任务”  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括许多其属性可以由属性表达式设置的任务。  
  
### <a name="analysis-services-execute-ddl-task"></a>Analysis Services 执行 DDL 任务  
 `SourceType` 属性-通过使用中的值设置`DDLSourceType`枚举。  
  
|DDLSourceType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|文件连接|@shouldalert|  
|变量|2|  
  
### <a name="bulk-insert-task"></a>大容量插入任务  
 `DataFileType` 属性-通过使用中的值设置`DTSBulkInsert_DataFileType`枚举。  
  
|DTSBulkInsert_DataFileType 中的友好名称|数值|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|@shouldalert|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>执行 SQL 任务  
 `ResultSetType` 属性-通过使用中的值设置`ResultSetType`枚举。  
  
|ResultSetType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|ResultSetType_None|@shouldalert|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType` 属性-通过使用中的值设置`SqlStatementSourceType`枚举。  
  
|SqlStatementSourceType 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|DirectInput|@shouldalert|  
|文件连接|2|  
|变量|3|  
  
### <a name="file-system-task"></a>文件系统任务  
 `Operation` 属性-通过使用中的值设置`DTSFileSystemOperation`枚举。  
  
|DTSFileSystemOperation 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|@shouldalert|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 `Attributes` 属性-通过使用中的值设置`DTSFileSystemAttributes`枚举。  
  
|DTSFileSystemAttributes 中的友好名称|数值|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|@shouldalert|  
|Hidden|2|  
|ReadOnly|4|  
|系统|8|  
  
### <a name="ftp-task"></a>FTP 任务  
 `Operation` 属性-通过使用中的值设置`DTSFTPOp`枚举。  
  
|DTSFTPOp 中的友好名称|数值|  
|-------------------------------|-------------------|  
|Send|0|  
|Receive|@shouldalert|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType` 属性-通过使用中的值设置`MQMessageType`枚举。  
  
|MQMessageType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|@shouldalert|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType` 属性-通过使用中的值设置`MQStringMessageCompare`枚举。  
  
|MQStringMessageCompare 中的友好名称|数值|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|@shouldalert|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType` 属性-通过使用中的值设置`MQType`枚举。  
  
|MQType 中的友好名称|数值|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|@shouldalert|  
  
### <a name="send-mail-task"></a>发送邮件任务  
 `MessageSourceType` 属性-通过使用中的值设置`SendMailMessageSourceType`枚举。  
  
|SendMailMessageSourceType 中的友好名称|数值|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|文件连接|@shouldalert|  
|变量|2|  
  
 `Priority` 属性-通过使用中的值设置`MailPriority`枚举。  
  
|MailPriority 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|High|@shouldalert|  
|Normal|3|  
|Low|5|  
  
### <a name="transfer-database-task"></a>传输数据库任务  
 `Action` 属性-通过使用中的值设置`TransferAction`枚举。  
  
|TransferAction 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|复制|0|  
|“移动”|@shouldalert|  
  
 `Method` 属性-通过使用中的值设置`TransferMethod`枚举。  
  
|TransferMethod 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|@shouldalert|  
  
### <a name="transfer-error-messages-task"></a>传输错误消息任务  
 `IfObjectExists` 属性-通过使用中的值设置`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|@shouldalert|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>传输作业任务  
 `IfObjectExists` 属性-通过使用中的值设置`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|@shouldalert|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>传输登录名任务  
 `IfObjectExists` 属性-通过使用中的值设置`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|@shouldalert|  
|Skip|2|  
  
 `LoginsToTransfer` 属性-通过使用中的值设置`LoginsToTransfer`枚举。  
  
|LoginsToTransfer 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|@shouldalert|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>传输主存储过程任务  
 `IfObjectExists` 属性-通过使用中的值设置`IfObjectExists`枚举。  
  
|IfObjectExists 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|@shouldalert|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>传输 SQL Server 对象任务  
 `ExistingData` 属性-通过使用中的值设置`ExistingData`枚举。  
  
|ExistingData 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|替换|0|  
|追加|@shouldalert|  
  
### <a name="web-service-task"></a>Web 服务任务  
 `OutputType` 属性-通过使用中的值设置`DTSOutputType`枚举。  
  
|DTSOutputType 中的友好名称|数值|  
|------------------------------------|-------------------|  
|文件|0|  
|变量|@shouldalert|  
  
### <a name="wmi-data-reader-task"></a>WMI 数据读取器任务  
 `OverwriteDestination` 属性-通过使用中的值设置`OverwriteDestination`枚举。  
  
|OverwriteDestination 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|@shouldalert|  
|KeepOriginal|2|  
  
 `OutputType` 属性-通过使用中的值设置`OutputType`枚举。  
  
|OutputType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|@shouldalert|  
|PropertyNameAndValue|2|  
  
 `DestinationType` 属性-通过使用中的值设置`DestinationType`枚举。  
  
|DestinationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|变量|@shouldalert|  
  
 `WqlQuerySourceType` 属性-通过使用中的值设置`QuerySourceType`枚举。  
  
|QuerySourceType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|DirectInput|@shouldalert|  
|变量|2|  
  
 WMI 事件观察器 `ActionAtEvent` 属性 - 通过使用 `ActionAtEvent` 枚举中的值设置。  
  
|ActionAtEvent 中的友好名称|数值|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|@shouldalert|  
  
 `ActionAtTimeout` 属性-通过使用中的值设置`ActionAtTimeout`枚举。  
  
|ActionAtTimeout 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|@shouldalert|  
  
 `AfterEvent` 属性-通过使用中的值设置`AfterEvent`枚举。  
  
|AfterEvent 中的友好名称|数值|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|@shouldalert|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout` 属性-通过使用中的值设置`AfterTimeout`枚举。  
  
|AfterTimeout 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|@shouldalert|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType` 属性-通过使用中的值设置`QuerySourceType`枚举。  
  
|QuerySourceType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|文件连接|0|  
|DirectInput|@shouldalert|  
|变量|2|  
  
### <a name="xml-task"></a>XML 任务  
 `OperationType` 属性-通过使用中的值设置`DTSXMLOperation`枚举。  
  
|DTSXMLOperation 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|验证|0|  
|XSLT|@shouldalert|  
|XPATH|2|  
|合并|3|  
|差异|4|  
|Patch|5|  
  
 `SourceType`、`SecondOperandType` 和 `XPathSourceType` 属性 - 通过使用 `DTSXMLSourceType` 枚举中的值设置。  
  
|DTSXMLSourceType 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|文件连接|0|  
|变量|@shouldalert|  
|DirectInput|2|  
  
 `DestinationType` 并**DiffGramDestinationType**属性-通过使用中的值设置`DTSXMLSaveResultTo`枚举。  
  
|DTSXMLSaveResultTo 中的友好名称|数值|  
|-----------------------------------------|-------------------|  
|文件连接|0|  
|变量|@shouldalert|  
  
 `ValidationType` 属性-通过使用中的值设置`DTSXMLValidationType`枚举。  
  
|DTSXMLValidationType 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|@shouldalert|  
  
 `XPathOperation` 属性-通过使用中的值设置`DTSXMLXPathOperation`枚举。  
  
|DTSXMLXPathOperation 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|值|@shouldalert|  
|NodeList|2|  
  
 `DiffOptions` 属性-通过使用中的值设置`DTSXMLDiffOptions`枚举。 此枚举器中的选项不相互排斥。 若要使用多个选项，请将要应用的选项作为逗号分隔的列表提供。  
  
|DTSXMLDiffOptions 中的友好名称|数值|  
|----------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|IgnoreChildOrder|@shouldalert|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm` 属性-通过使用中的值设置`DTSXMLDiffAlgorithm`枚举。  
  
|DTSXMLDiffAlgorithm 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|Auto|0|  
|Fast|@shouldalert|  
|Precise|2|  
  
##  <a name="MaintenancePlanTasks"></a> 维护计划任务  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括的一组任务将执行在维护计划和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中使用的 SQL Server 任务。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持通过编程来使用这些任务，而且编程参考文档不包括这些任务及其枚举器的 API 文档。  
  
### <a name="all-maintenance-tasks"></a>所有维护任务  
 所有维护任务均使用以下枚举来设置指定的属性。  
  
 `DatabaseSelectionType` 属性-通过使用中的值设置`DatabaseSelection`枚举。  
  
|DatabaseSelection 中的友好名称|数值|  
|----------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|All|@shouldalert|  
|系统|2|  
|用户|3|  
|Specific|4|  
  
 `TableSelectionType` 属性-通过使用中的值设置`TableSelection`枚举。  
  
|TableSelection 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|All|@shouldalert|  
|Specific|2|  
  
 `ObjectTypeSelection` 属性-通过使用中的值设置`ObjectType`枚举。  
  
|ObjectType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|表|0|  
|“查看”|@shouldalert|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>“备份数据库”任务  
 `DestinationCreationType` 属性-通过使用中的值设置`DestinationType`枚举。  
  
|DestinationType 中的友好名称|数值|  
|--------------------------------------|-------------------|  
|Auto|0|  
|Manual|@shouldalert|  
  
 `ExistingBackupsAction` 属性-通过使用中的值设置`ActionForExistingBackups`枚举。  
  
|ActionForExistingBackups 中的友好名称|数值|  
|-----------------------------------------------|-------------------|  
|追加|0|  
|Overwrite|@shouldalert|  
  
 `BackupAction` 属性-通过使用中的值设置`BackupTaskType`枚举。 此属性适用于`BackupIsIncremental`属性来定义该任务执行的备份类型。  
  
|BackupTaskType 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|“数据库”|0|  
|“文件”|@shouldalert|  
|日志|2|  
  
 `BackupDevice` 属性 - 通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) `DeviceType` 枚举中的值设置。  
  
|DeviceType 中的友好名称|数值|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|磁带|@shouldalert|  
|文件|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>“清除维护”任务  
 `FileTypeSelected` 属性-通过使用中的值设置`FileType`枚举。  
  
|FileType 中的友好名称|数值|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|@shouldalert|  
  
 `OlderThanTimeUnitType` 属性-通过使用中的值设置`TimeUnitType`枚举。  
  
|TimeUnitType 中的友好名称|数值|  
|-----------------------------------|-------------------|  
|Day|0|  
|Week|@shouldalert|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>“更新统计信息”任务  
 `UpdateType` 属性 - 通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) `StatisticsTarget` 枚举中的值设置。  
  
|StatisticsTarget 中的友好名称|数值|  
|---------------------------------------|-------------------|  
|“列”|@shouldalert|  
|索引|2|  
|All|3|  
  
##  <a name="CommonProperties"></a> 通用属性  
 包、任务和 Foreach 循环、For 循环和序列容器可以使用以下枚举来设置指定的属性。  
  
 `ForceExecutionResult` 属性-通过使用中的值设置`DTSForcedExecResult`枚举。  
  
|DTSForcedExecResult 中的友好名称|数值|  
|------------------------------------------|-------------------|  
|InclusionThresholdSetting|-1|  
|成功|0|  
|失败|@shouldalert|  
|Completion|2|  
  
 `IsolationLevel` 属性 - 由 .NET Framework `IsolationLevel` 枚举设置。 详细信息，请参阅位于 [MSDN Library](http://go.microsoft.com/fwlink?LinkId=17313)中的 .NET Framework 类库。  
  
 `LoggingMode` 属性-通过使用中的值设置`DTSLoggingMode`枚举。  
  
|DTSLoggingMode 中的友好名称|数值|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|已启用|@shouldalert|  
|禁用|2|  
  
 `TransactionOption` 属性-通过使用中的值设置`DTSTransactionOption`枚举。  
  
|DTSTransactionOption 中的友好名称|数值|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|是否支持|@shouldalert|  
|Required|2|  
  
## <a name="related-tasks"></a>Related Tasks  
 [添加或更改属性表达式](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>请参阅  
 [在包中使用属性表达式](use-property-expressions-in-packages.md)   
 [Integration Services &#40;SSIS&#41;包](../integration-services-ssis-packages.md)   
 [Integration Services 容器](../control-flow/integration-services-containers.md)   
 [Integration Services 任务](../control-flow/integration-services-tasks.md)   
 [优先约束](../control-flow/precedence-constraints.md)  
  
  
