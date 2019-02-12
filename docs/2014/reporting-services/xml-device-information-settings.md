---
title: XML 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7aa0f6e28dae59d7559dbb009ce4441dd4a2119d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013138"
---
# <a name="xml-device-information-settings"></a>XML 设备信息设置
  下表列出以 XML 格式呈现时的设备信息设置。  
  
|设置|ReplTest1|  
|-------------|-----------|  
|`XSLT`|要应用于 XML 文件的 XSLT 的报表服务器命名空间中的路径，例如 `/Transforms/myxslt`。 该 xsl 文件必须是报表服务器上的已发布资源，并且您必须通过报表服务器项路径访问它。 将在报表中指定的 XSLT 之后应用此设置的值。 如果应用 `XSLT` 设置，则将忽略 `OmitSchema` 设置。|  
|**MIMEType**|XML 文件的多用途 Internet 邮件扩展 (MIME) 类型。|  
|**UseFormattedValues**|指示在生成 XML 数据时是否呈现文本框的格式化值。 如果值为 false，则指示使用文本框的基础值。|  
|**Indented**|指示是否生成缩进的 XML。 默认值 `false` 生成非缩进的压缩 XML。|  
|`OmitNamespace`|指示是否从 XML 中忽略默认命名空间。<br /><br /> 如果为 true，则 XML 未指定默认命名空间。<br /><br /> 如果为 false，则 XML 使用报表的 DataSchema 属性值指定默认命名空间。 该 DataSchema 属性默认为报表名称。<br /><br /> 默认值是 `false`。|  
|`OmitSchema`|指示是否从 XML 中忽略架构位置。 该位置为 SchemaLocation 属性。 OmitSchema 的默认值依赖于 OmitNamespace 的值：<br /><br /> 如果 OmitNamespace = False，则默认 OmitSchema = `False`。 用户可以通过设置 OmitSchema = True，覆盖该默认值。<br /><br /> 如果 OmitNamespace = True，则 OmitSchema 将起到 `True` 的作用，无论为 OmitShema 显式配置的值如何。|  
|**编码**|.NET Framework 支持的字符编码的 Internet 编号分配机构 (IANA) 名称。 默认值是 `UTF-8`。 其他值的示例包括 ASCII、UTF-7 和 UTF-16。|  
|**FileExtension**|所生成的文件使用的文件扩展名。|  
|**架构**|指示是否呈现 XML 架构定义 (XSD) 或是否呈现实际 XML 数据。 值为 `true` 指示将呈现 XML 架构。 默认值是 `false`。|  
  
## <a name="see-also"></a>请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
