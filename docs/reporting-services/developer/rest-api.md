---
title: 使用 Reporting Services 的 REST API 进行开发 | Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 05/25/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: developer
ms.topic: conceptual
author: markingmyname
ms.author: maghan
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e566f09ae6c3357ecdbc2083f1f32fffadcf94d0
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028228"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>使用 Reporting Services 的 REST API 进行开发

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services 支持表述性状态转移 (REST) API。 REST API 是支持一组 HTTP 操作（方法）的服务终结点，它们提供针对报表服务器中资源的创建、检索、更新或删除访问权限。

REST API 提供对 SQL Server 2017 Reporting Services 报表服务器目录中对象的编程访问。 对象包括文件夹、报表、KPI、数据源、数据集、刷新计划、订阅等等。 例如，使用 REST API 可以导航文件夹层次结构、发现文件夹的内容或下载报表定义。 此外还可创建、更新和删除对象。 有关对象使用的例子包括上载报表、执行刷新计划、删除文件夹等等。

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>REST API 请求/响应的组件

REST API 请求/响应对可分解为五个组件：

* **请求 URI**，其中包括：`{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`。 虽然请求 URI 包含在请求消息标头中，但此处将单独进行调用，因为大多数语言或框架都要求将其与请求消息分开传递。

    * URI 方案：指示用于传输请求的协议。 例如，`http` 或 `https`。
    * URI 主机：指定承载 REST 服务终结点的服务器域名或 IP 地址，例如 `myserver.contoso.com`。
    * 资源路径：指定资源或资源集合，其中可能包含服务在做资源抉择时使用的多个段。 例如：`CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` 可用于获取 CatalogItem 的指定属性。
    * 查询字符串（可选）：提供其他简单参数，例如 API 版本或资源选择条件。

* HTTP 请求消息标头字段：

    * 所需的 [ HTTP 方法](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)（也称为操作或谓词），它告知该服务你请求的操作类型。 Reporting Services REST API 支持 DELETE、GET、HEAD、PUT、POST 和 PATCH 方法。
    * 指定的 URI 和 HTTP 方法所需的其他可选的标头字段。

* 可选的 HTTP 请求消息正文字段，用于支持 URI 和 HTTP 操作。 例如，POST 操作包含作为复杂参数传递的 MIME 编码对象。 对于 POST 或 PUT 操作，还应在 `Content-type` 请求标头中指定正文的 MIME 编码类型。 某些服务要求使用特定的 MIME 类型，如 `application/json`。

* HTTP 响应消息标头字段：

    * [HTTP 状态代码](http://www.w3.org/Protocols/HTTP/HTRESP.html)，包括从 2xx 成功代码到 4xx 或 5xx 错误代码在内的各种代码。 或者，可能返回服务定义的状态代码，如 API 文档中所指示。
    * 可选的其他标头字段，用于支持请求的响应，例如 `Content-type` 响应标头。

* 可选的 HTTP 响应消息正文字段：

    * 在 HTTP 响应正文中返回 MIME 编码的响应对象，例如来自返回数据的 GET 方法的响应。 通常，这些对象以结构化格式（如 JSON 或 XML）返回，如 `Content-type` 响应标头所指示。

## <a name="api-documentation"></a>API 文档

新式 REST API 需要新式 API 文档。 REST API 基于 OpenAPI 规范（又名 swagger 规范） 文档可从 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) 上获取。 除记录 API 外，SwaggerHub 还帮助在选择的语言中生成客户端库 - JavaScript、TypeScript、C#、Java、Python、Ruby 等。

## <a name="testing-api-calls"></a>测试 API 调用

一个用于测试 HTTP 请求/响应消息的工具是 [Fiddler](http://www.telerik.com/fiddler)。 Fiddler 是一个免费的 Web 调试代理，可以拦截 REST 请求，以便诊断 HTTP 请求/响应消息。

## <a name="next-steps"></a>后续步骤

在 [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0) 上查看可用的 API。

可在 [GitHub](https://github.com/Microsoft/Reporting-Services) 上找到示例。 该示例包含一个基于 TypeScript、React、webpack 构建的 HTML5 应用以及一个 PowerShell 示例。

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
