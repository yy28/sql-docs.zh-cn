---
title: "XML 设备信息设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a5af7c3ba8de8f3134e40850524ecfd397faebd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="xml-device-information-settings"></a>XML 设备信息设置
  下表列出以 XML 格式呈现时的设备信息设置。  
  
|设置|值|详细信息|  
|-------------|------------|-------------|  
|**XSLT**|要应用于 XML 文件的 XSLT 的报表服务器命名空间中的路径，例如 **/Transforms/myxslt**。|该 xsl 文件必须是报表服务器上的已发布资源，并且您必须通过报表服务器项路径访问它。 将在报表中指定的 XSLT 之后应用此设置的值。 如果应用了 **XSLT** 设置，将忽略 **OmitSchema** 设置。|  
|**MIMEType**|XML 文件的多用途 Internet 邮件扩展 (MIME) 类型。||  
|**UseFormattedValues**|**true**<br /><br /> **false**|指示在生成 XML 数据时是否呈现文本框的格式化值。<br /><br /> 如果值为 false，则指示使用文本框的基础值。|  
|**Indented**|**true**<br /><br /> **false**|指示是否生成缩进的 XML。 默认值 **false** 会生成非缩进的压缩 XML。|  
|**OmitNamespace**|**true**<br /><br /> **false**|指示是否从 XML 中忽略默认命名空间。<br /><br /> 如果为 true，则 XML 未指定默认命名空间。<br /><br /> 如果为 false，则 XML 使用报表的 DataSchema 属性值指定默认命名空间。 该 DataSchema 属性默认为报表名称。<br /><br /> 默认值是**false**。|  
|**OmitSchema**|**true**<br /><br /> **false**|指示是否从 XML 中忽略架构位置。 该位置为 SchemaLocation 属性。<br /><br /> OmitSchema 的默认值依赖于 OmitNamespace 的值：<br /><br /> 如果 OmitNamespace = False，则默认情况下 OmitSchema = **False** 。 用户可以通过设置 OmitSchema = True，覆盖该默认值。<br /><br /> 如果 OmitNamespace = True，则 OmitSchema 可充当 **True** ，无论为 OmitShema 显式配置的值如何。|  
|**编码**|.NET Framework 支持的字符编码的 Internet 编号分配机构 (IANA) 名称。|默认值为 **UTF-8**。 其他值的示例包括 ASCII、UTF-7 和 UTF-16。|  
|**FileExtension**|所生成的文件使用的文件扩展名。||  
|**架构**|值为 **true** 指示将呈现 XML 架构。 默认值是 **false**。|指示是否呈现 XML 架构定义 (XSD) 或是否呈现实际 XML 数据。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [自定义在 RSReportServer.Config 中的呈现扩展插件参数](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 &#40;SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  

