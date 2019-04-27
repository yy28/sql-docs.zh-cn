---
title: 记录属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5ade1c582956548a62f36d79f0e1b8fbd03525a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746869"
---
# <a name="log-properties"></a>日志属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的日志服务器属性 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
## <a name="general"></a>常规  
 `File`  
 一个字符串属性，用于标识服务器日志文件的名称。 只有在使用磁盘文件进行日志记录时，此属性才适用，而在使用数据库表进行日志记录时（默认行为）并不适用。  
  
 此属性的默认值为 msmdsrv.log。  
  
 `FileBufferSize`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `MessageLogs`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="error-log"></a>错误日志  
 您可以在服务器实例级别设置这些属性以修改其他工具和设计器中显示的“错误配置”的默认值。 请参阅[多维数据集、 分区和维度处理的错误配置&#40;SSAS-多维&#41;](../multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)并<xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A>有关详细信息。  
  
 **ErrorLog\ErrorLogFileName**  
 在服务器执行处理操作期间使用的一个默认属性。  
  
 **ErrorLog\ErrorLogFileSize**  
 在服务器执行处理操作期间使用的一个默认属性。  
  
 **ErrorLog\KeyErrorAction**  
 指定发生 `KeyNotFound` 错误时服务器执行的操作。 对此错误的有效响应包括：  
  
-   `ConvertToUnknown` 指示服务器将错误键值分配给未知成员。  
  
-   `DiscardRecord` 指示服务器排除该记录。  
  
 **ErrorLog\KeyErrorLogFile**  
 这是用户定义的文件名，必须具有 .log 文件扩展名，位于服务帐户拥有读/写权限的文件夹中。 此日志文件仅包含处理期间生成的错误。 如果您需要详细信息，请使用网络流量记录器。  
  
 **ErrorLog\KeyErrorLimit**  
 这是在处理失败前服务器将允许的最大数据完整性错误数目。 值为 -1 表示没有限制。 默认值为 0，表示处理在发生第一个错误时停止。 您还可以将其设置为整数。  
  
 **ErrorLog\KeyErrorLimitAction**  
 指定键错误数目达到上限时服务器所执行的操作。 对此操作的有效响应包括：  
  
-   `StopProcessing` 指示服务器在达到错误限制时停止处理。  
  
-   `StopLogging` 指示服务器在达到错误限制时停止记录错误，但允许继续处理。  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 指定发生 `KeyNotFound` 错误时服务器执行的操作。 对此错误的有效响应包括：  
  
-   `IgnoreError` 指示服务器继续处理而不记录错误或一直计数至键错误限制。 通过忽略该错误，您可以继续处理而不会增加错误计数或将错误记录至屏幕或日志文件。 有关记录具有数据完整性问题，无法添加到数据库。 该记录或者将被弃用，或者聚合到未知成员，具有情况由 `KeyErrorAction` 属性确定。  
  
-   `ReportAndContinue` 指示服务器记录错误、一直将错误计数至键错误限制并继续处理。 触发错误的记录被弃用或转换为未知成员。  
  
-   `ReportAndStop` 指示服务器记录错误并立即停止处理，而不管键错误限制如何。 触发错误的记录被弃用或转换为未知成员。  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 指定发现重复键时服务器所执行的操作。 `IgnoreError`有效值包括用于继续处理（就好像该错误没有发生）的 `ReportAndContinue`、用于记录错误并继续处理的 `ReportAndStop` 以及用于记录错误并立即停止处理（即使错误计数低于错误限制）的 。  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 指定在将 Null 键转换为未知成员后服务器所执行的操作。 `IgnoreError`有效值包括用于继续处理（就好像该错误没有发生）的 `ReportAndContinue`、用于记录错误并继续处理的 `ReportAndStop` 以及用于记录错误并立即停止处理（即使错误计数低于错误限制）的 。  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 指定 `NullProcessing` 针对维度属性设置为 `Error` 时服务器执行的操作。 给定属性中不允许有 Null 值时，将生成错误。 此错误配置属性会通知下一步报告该错误，并继续进行处理，直至达到错误限制。 `IgnoreError`有效值包括用于继续处理（就好像该错误没有发生）的 `ReportAndContinue`、用于记录错误并继续处理的 `ReportAndStop` 以及用于记录错误并立即停止处理（即使错误计数低于错误限制）的 。  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 在服务器执行处理操作期间使用的一个默认属性。  
  
 **ErrorLog\IgnoreDataTruncation**  
 在服务器执行处理操作期间使用的一个默认属性。  
  
## <a name="exception"></a>异常  
 **Exception\CreateAndSendCrashReports**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Exception\CrashReportsFolder**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Exception\SQLDumperFlagsOn**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Exception\SQLDumperFlagsOff**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Exception\MiniDumpFlagsOn**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Exception\MinidumpErrorList**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="flight-recorder"></a>网络流量记录器  
 **FlightRecorder\Enabled**  
 一个布尔值属性，它指示是否启用网络流量记录器功能。  
  
 **FlightRecorder\FileSizeMB**  
 一个有符号 32 位整数属性，它定义网络流量记录器磁盘文件大小 (MB)。  
  
 **FlightRecorder\LogDurationSec**  
 一个有符号 32 位整数属性，它定义网络流量记录器的翻转频率（秒）。  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 一个字符串属性，它定义快照定义文件（该文件包含拍摄快照时向服务器发出的发现命令）的名称。  
  
 此属性的默认值为空，表示默认文件名为 FlightRecorderSnapshotDef.xml。  
  
 **FlightRecorder\SnapshotFrequencySec**  
 一个有符号 32 位整数属性，它定义快照频率（秒）。  
  
 **FlightRecorder\TraceDefinitionFile**  
 一个字符串属性，它指定网络流量记录器跟踪定义文件的名称。  
  
 此属性的默认值为空，表示默认文件名为 FlightRecorderTraceDef.xml。  
  
## <a name="query-log"></a>查询日志  
 **适用范围：** 仅限多维服务器模式  
  
 **QueryLog\QueryLogFileName**  
 一个字符串属性，它指定查询日志文件的名称。 只有在使用磁盘文件进行日志记录时，此属性才适用，而在使用数据库表进行日志记录时（默认行为）并不适用。  
  
 **QueryLog\QueryLogSampling**  
 一个有符号 32 位整数属性，它指定查询日志抽样率。  
  
 此属性的默认值为 10，表示每 10 个服务器查询记录一个。  
  
 **QueryLog\QueryLogFileSize**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **QueryLog\QueryLogConnectionString**  
 一个字符串属性，它指定到查询日志数据库的连接。  
  
 **QueryLog\QueryLogTableName**  
 一个字符串属性，它指定查询日志表的名称。  
  
 此属性的默认值为 OlapQueryLog。  
  
 **QueryLog\CreateQueryLogTable**  
 一个布尔值属性，它指定是否创建查询日志表。  
  
 此属性的默认值为 false，指示服务器不会自动创建日志表，并且不记录查询事件。  
  
> [!NOTE]  
>  有关配置查询日志的详细信息，请参阅[Analysis Services 中记录操作](../instances/log-operations-in-analysis-services.md)。  
  
## <a name="trace"></a>跟踪  
 **Trace\TraceBackgroundDistributionPeriod**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceBackgroundFlushPeriod**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceFileBufferSize**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceMaxRowsetSize**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceProtocolTraffic**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceReportFQDN**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceRequestParameters**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
