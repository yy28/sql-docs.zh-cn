---
title: WMI 数据读取器任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3d0262328fd3f5a2ed948fb8f2c62781dc19ae17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229777"
---
# <a name="wmi-data-reader-task"></a>WMI 数据读取器任务
  WMI 数据读取器任务使用 Windows Management Instrumentation (WMI) 查询语言来运行查询，此查询语言从 WMI 返回有关计算机系统的信息。 可以将 WMI 数据读取器任务用于下列目的：  
  
-   查询本地或远程计算机上的 Windows 事件日志并将此信息写入文件或变量。  
  
-   获取有关硬件组件的存在、状态或属性的信息，然后使用此信息决定控制流中的其他任务是否应该运行。  
  
-   获取应用程序的列表，并确定每个应用程序安装的是何种版本。  
  
 可以通过以下方式配置 WMI 数据读取器任务：  
  
-   指定要使用的 WMI 连接管理器。  
  
-   指定 WQL 查询的源。 查询可以存储在任务属性中，也可以存储在任务之外的变量或文件中。  
  
-   定义 WQL 查询结果的格式。 该任务支持表、属性名称/值对或属性值三种格式。  
  
-   指定查询目标。 目标可以是变量或文件。  
  
-   指示覆盖、保留还是追加查询目标。  
  
 如果源或目标是文件，则 WMI 数据读取器任务使用文件连接管理器连接到该文件。 有关详细信息，请参阅 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 WMI 数据读取器任务使用 WMI 连接管理器连接到该任务从中读取 WMI 信息的服务器。 有关详细信息，请参阅 [WMI Connection Manager](../connection-manager/wmi-connection-manager.md)。  
  
## <a name="wql-query"></a>WQL 查询  
 WQL 是 SQL 的方言，其扩展插件支持 WMI 事件通知和其他 WMI 特定功能。 有关 WQL 的详细信息，请参阅 [MSDN Library](http://go.microsoft.com/fwlink/?linkid=7022)中的 Windows Management Instrumentation 文档。  
  
> [!NOTE]  
>  WMI 类因 Windows 版本的不同而异。  
  
 下列 WQL 查询返回应用程序日志事件中的项。  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 下列 WQL 查询返回逻辑磁盘信息。  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 下列 WQL 查询返回操作系统的快速修补工程 (QFE) 更新列表。  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>WMI 数据读取器任务可用的自定义日志记录消息  
 下表列出了 WMI 数据读取器任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../custom-messages-for-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|指示任务已开始读取 WMI 数据。|  
|`WMIDataReaderOperation`|报告任务所运行的 WQL 查询。|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>配置 WMI 数据读取器任务  
 可以采用编程方式或通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请单击以下主题之一：  
  
-   [WMI 数据读取器任务编辑器&#40;WMI 选项页&#41;](../wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关以编程方式设置这些属性的信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)  
  
  
