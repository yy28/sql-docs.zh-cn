---
title: RSReportDesigner 配置文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], configuration file
- RSReportDesigner configuration file
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ad5a5660e642c13a604b9fdb1a7e5aac516686ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211699"
---
# <a name="rsreportdesigner-configuration-file"></a>RSReportDesigner 配置文件
  RSReportDesigner.config 文件存储有关可用于报表设计器的呈现扩展插件和数据处理扩展插件的设置。 数据处理扩展插件信息存储在`Data`元素。 呈现扩展插件信息存储在 `Render` 元素中。 `Designer` 元素可枚举报表设计器中所用的查询生成器。  
  
 报表设计器使用嵌入的报表服务器功能来预览报表。 您可以指定服务器相关设置，以支持预览操作的本地服务器端处理过程。 有关报表服务器配置设置的详细信息，请参阅[RSReportServer 配置文件](rsreportserver-config-configuration-file.md)。  
  
## <a name="file-location"></a>文件位置  
 此文件位于 \Program Files\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies 中。  
  
## <a name="editing-guidelines"></a>编辑指南  
 除非您要部署或删除自定义扩展插件、禁用预览过程中的缓存功能或在升级 Service Pack 后注册新的数据处理扩展插件，否则请不要修改此文件中的设置。  
  
 若要自定义呈现扩展插件设置，则可使用编辑配置文件的特定说明。 有关详细信息，请参阅[在 RSReportServer.Config 中自定义呈现扩展插件参数](../customize-rendering-extension-parameters-in-rsreportserver-config.md)。  
  
 有关如何编辑配置文件的常规说明，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
## <a name="example-configuration-file"></a>示例配置文件  
 下面的示例说明了 RSReportDesigner.config 文件的格式。  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## <a name="configuration-settings"></a>配置设置  
  
|设置|Description|  
|-------------|-----------------|  
|`SecureConnectionLevel`|指定 Web 服务连接的安全级别。 有效值的范围为 0 到 3 之间，其中 0 的安全性最低。 有关详细信息，请参阅 [Using Secure Web Service Methods](../report-server-web-service/net-framework/using-secure-web-service-methods.md)。|  
|`InstanceName`|预览服务器的标识符。 不要修改此值。|  
|`SessionCookies`|指定报表服务器是否使用浏览器 cookie 维持会话信息。 有效的值包括`true`和`false`。 默认值为 `true`。 如果将此值设置为 False，会话数据将存储在 **reportservertempdb** 数据库中。|  
|`SessionTimeoutMinutes`|指定会话 cookie 的有效期。 默认为 3 分钟。|  
|`PolicyLevel`|指定安全策略配置文件。 有效的值为 Rspreviewpolicy.config。有关详细信息，请参阅 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)。|  
|`CacheDataForPreview`|如果设置为`True`，报表设计器将数据存储在本地计算机上的缓存文件中。 有效的值为`True`（默认值） 和`False`。 有关详细信息，请参阅 [Previewing Reports](../reports/previewing-reports.md)。|  
|`Render`|枚举报表设计器可用于进行预览操作的呈现扩展插件。 用于预览的呈现扩展插件组应该与随报表服务器安装的呈现扩展插件组相同。<br /><br /> `Name` 指定呈现扩展插件。 如果您通过代码调用呈现扩展插件，请使用该值来调用特定的扩展插件。<br /><br /> `Type` 指定扩展类的完全限定的类名以及库名，以逗号分隔。<br /><br /> `Visible` 指定是否在相应的用户界面中显示该名称。 此值可以是`True`（默认值） 或`False`。 如果为 `True`，则该名称将在相应的用户界面中显示。|  
|`Data`|枚举报表设计器可用于连接为报表提供数据的数据源的数据处理扩展插件。 在报表设计器中使用的数据处理扩展插件组可能与随报表服务器安装的数据处理扩展插件组相同。 如果正在添加或删除自定义扩展插件，请参阅[部署数据处理扩展插件](../extensions/data-processing/deploying-a-data-processing-extension.md)。<br /><br /> `Name` 指定数据处理扩展插件。<br /><br /> `Type` 指定扩展类的完全限定的类名以及库名，以逗号分隔。|  
|`Designer`|枚举报表设计器可用的查询生成器。 查询生成器提供了一个用户界面，用于构造检索在报表中使用的数据的查询。 查询生成器因数据处理扩展插件的不同而有所不同。 默认情况下，Reporting Services 为产品中包含的所有数据处理扩展插件提供了一个直观数据工具用户界面。 不过，如果您生成或使用第三方数据处理扩展插件，可能要应用其他查询生成器界面。|  
|`PreviewProcessingServiceStartupTimeoutSeconds`|指定在显示错误消息前等待预览处理服务启动的时间。 默认值为 15 秒。|  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置文件](reporting-services-configuration-files.md)   
 [查询设计工具在报表设计器的 SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)  
  
  
