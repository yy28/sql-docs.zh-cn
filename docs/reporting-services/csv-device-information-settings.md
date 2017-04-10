---
title: "CSV 设备信息设置 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CSV [Reporting Services]"
  - "设备信息设置 [Reporting Services], CSV 呈现"
ms.assetid: f96f83a6-50bc-48ce-9fcd-fd9e1952d40a
caps.latest.revision: 43
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 43
---
# CSV 设备信息设置
  通过用于 CSV 呈现扩展插件的设备信息设置，可以更改分隔符和限定符并指定换行符处理。 还可以提交文件的扩展名，以及指示编码和是否在输出中包括标题行。 由于分隔符可能是特殊字符，因此，如果将设置编写为 XML，则应在 CDATA 部分对它们进行编码。  
  
 下表列出以文本格式呈现时的设备信息设置。  
  
|设置|“值”|  
|-------------|-----------|  
|**编码**|.NET Framework 支持的字符编码的 Internet 编号分配机构 (IANA) 名称。 默认值为 **UTF-8**。 其他值的示例包括 ASCII、UTF-7 和 UTF-16。|  
|**ExcelMode**|指定目标输出面向 Excel。 默认值为 **true**。|  
|**FieldDelimiter**|要放入结果中的分隔符字符串。 默认值为逗号 (,)。 当您在 URL 中传递此设备信息的值时，应对该值进行 URL 编码。 例如，作为分隔符的制表符应为“%09”。<br /><br /> 可通过在配置文件中更改设备信息设置将默认字段分隔符更改为任何所需的字符，包括 TAB。 例如，若要使用 TAB，请将 FieldDelimiter 设置更改为 \<FieldDelimiter xml:space="preserve">[TAB]\</FieldDelimiter><br /><br /> 在此示例中，[TAB] 是实际的制表符，它表示在配置文件中将出现空白字符。 “xml:space”属性告诉分析器保留空白字符。|  
|**FileExtension**|要放入结果中的文件扩展名。 默认值是 **.CSV**秒。 如果同时指定了 **FileExtension** 和 **Extension** ，将优先使用 **FileExtension** 。|  
|**NoHeader**|指示是否从输出中排除标题行。 默认值是 **false**秒。|  
|**Qualifier**|围绕着包含字段分隔符或记录分隔符的结果放置的限定符字符串。 如果结果包含限定符，将重复此限定符。 **Qualifier** 设置必须与 **FieldDelimiter** 和 **RecordDelimiter** 设置不同。 默认值为引号 (")。|  
|**RecordDelimiter**|要放在每个记录末尾的记录分隔符。 默认值为 \<cr>\<lf>。|  
|**SuppressLineBreaks**|指示是否在输出中包含从数据删除的换行符。 默认值是 **false**秒。 如果值为 **true**，则 **FieldDelimiter**、 **RecordDelimiter**和 **Qualifier** 设置不能为空格字符。|  
|**UseFormattedValues**|指示是否将格式化的字符串放入 CSV 输出中。 默认值为 **true** （当 **ExcelMode** 为 **true**时），否则为 **false**。|  
  
## 另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  