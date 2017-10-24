---
title: "使用用于 Reporting Services 的 REST Api 开发 |Microsoft 文档"
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>使用 REST Api 开发的 Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 自 2017 年 Reporting Services 支持具象状态传输 (REST) Api。 REST Api 是支持 HTTP 操作 （方法），提供一组终结点创建的服务、 检索、 更新或删除报表服务器中的资源的访问权限。

REST API 提供对 SQL Server 自 2017 年 Reporting Services 报表服务器目录中的对象的编程访问。 对象的示例包括文件夹、 报表、 Kpi、 数据源、 数据集，刷新计划、 订阅和的详细信息。 REST API，可以使用，例如，文件夹层次结构中导航、 发现的一个文件夹中，内容或下载报表定义。 此外可以创建、 更新和删除对象。 对象使用的示例将报表上载、 执行刷新计划，删除文件夹，依次类推。

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 请求/响应的组件

REST API 请求/响应对可以分为五个组件：

* **请求 URI**，其中包括： `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`。 尽管请求 URI 包含在请求消息标头中，我们调出单独此处因为大多数语言或框架要求你单独将其传递从请求消息。

    * URI 方案： 指示用来传输请求的协议。 例如，`http`或`https`。
    * URI 主机： 指定的域名或 IP 地址的服务器托管的 REST 服务终结点的位置，如`myserver.contoso.com`。
    * 资源路径： 指定的资源或资源集合，其中可能包括由确定这些资源的选定内容中的服务的多个段。 例如：`CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties`可以用于获取指定的属性以 CatalogItem。
    * 查询字符串 （可选）： 提供附加的简单参数，如 API 版本或资源选择条件。

* HTTP 请求消息标头字段：

    * 必需[HTTP 方法](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)（也称为的操作或谓词），它指示该服务的所请求的操作的类型。 Reporting Services REST Api 支持删除，获取，HEAD、 PUT、 POST、 和修补程序方法。
    * 可选的其他标头字段，根据需要由指定的 URI 和 HTTP 方法。

* 可选 HTTP**请求消息正文**字段，以支持 URI 和 HTTP 操作。 例如，POST 操作包含作为复杂的参数传递的 MIME 编码对象。 对于 POST 或 PUT 操作，正文的 MIME 编码类型应指定在`Content-type`请求标头。 某些服务要求你使用特定的 MIME 类型，如`application/json`。

* HTTP**响应消息标头**字段：

    * [HTTP 状态代码](http://www.w3.org/Protocols/HTTP/HTRESP.html)、 涉及范围从 2xx 成功代码为 4xx 或 5xx 错误代码。 或者，定义服务的状态可能会返回代码，如 API 文档中所示。
    * 可选的其他标头字段，如需支持请求的响应，例如`Content-type`响应标头。

* 可选 HTTP**响应消息正文**字段：

    * HTTP 响应正文，如正在返回数据的 GET 方法从响应中返回 MIME 编码响应对象。 通常情况下，这些对象以结构化格式返回 JSON 或 XML，如所述`Content-type`响应标头。

## <a name="api-documentation"></a>API 文档

对于现代 API 文档，现代的 REST API 调用。 REST API （也称为基于 OpenAPI 规范 swagger 规范中） 上提供了文档和[SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)。 超出记录 API SwaggerHub 可帮助在选择 – JavaScript、 TypeScript、 C#、 Java、 Python、 Ruby 和的详细信息的语言中生成的客户端库。

## <a name="testing-api-calls"></a>测试 API 调用

是用于测试 HTTP 请求/响应消息的工具[Fiddler](http://www.telerik.com/fiddler)。 Fiddler 是一个免费 web 调试代理可以截获你 REST 请求，从而便于诊断 HTTP 请求 / 响应消息。

## <a name="next-steps"></a>后续步骤

通过上查看可用的 Api [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0)。

示例位于[GitHub](https://github.com/Microsoft/Reporting-Services)。 此示例包含基于 TypeScript、 响应和 PowerShell 示例 webpack 一个 HTML5 应用程序。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
