---
title: 使用大数据群集上的应用程序
titleSuffix: SQL Server big data clusters
description: 使用 RESTful web service (预览版) 在 SQL Server 2019 大数据群集上部署的应用程序。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419508"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>使用 RESTful web 服务, 使用部署在 SQL Server 大数据群集上的应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用 RESTful web 服务 (预览版) 来使用在 SQL Server 2019 大数据群集上部署的应用。

## <a name="prerequisites"></a>先决条件

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [mssqlctl 命令行实用工具](deploy-install-azdata.md)
- 使用[azdata](big-data-cluster-create-apps.md)或[应用部署扩展](app-deployment-extension.md)部署的应用

## <a name="capabilities"></a>功能

将应用程序部署到 SQL Server 2019 大数据群集 (预览版) 后, 可以使用 RESTful web 服务访问和使用该应用程序。 这样就可以将该应用程序与其他应用程序或服务 (例如, 移动应用或网站) 集成。 下表介绍了可用于**azdata**的应用程序部署命令, 以获取有关应用程序的 RESTful web 服务的信息。

|Command |描述 |
|:---|:---|
|`azdata app describe` | 描述应用程序。 |

可以获取有关`--help`参数的帮助, 如以下示例中所示:

```bash
azdata app describe --help
```

以下各节介绍如何检索应用程序的终结点, 以及如何使用 RESTful web 服务进行应用程序集成。

## <a name="retrieve-the-endpoint"></a>检索终结点

**Azdata 应用描述**命令提供了有关应用的详细信息, 包括群集中的终结点。 应用开发人员通常使用此方法来生成使用 swagger 客户端的应用, 并使用 webservice 以 RESTful 的方式与应用进行交互。

通过运行类似于下面的命令来描述你的应用程序:

```bash
azdata app describe --name addpy --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

请注意输出中的`10.1.1.3` IP 地址 (此示例中为) 和`30777`端口号 ()。

## <a name="generate-a-jwt-access-token"></a>生成 JWT 访问令牌

为了访问已部署的应用的 RESTful web 服务, 必须首先生成 JWT 访问令牌。 在浏览器中打开以下 URL: `https://[IP]:[PORT]/api/docs/swagger.json`使用在上面的`describe`命令中运行的 IP 地址和端口。 你将必须使用你用来`azdata login`登录的同一凭据登录。

将`swagger.json`的内容粘贴到[Swagger 编辑器](https://editor.swagger.io)中, 以了解可用的方法:

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

`token`请注意`app` GET 方法和 POST 方法。 由于应用程序的身份验证使用 JWT 令牌, 因此你将需要使用你喜欢的工具获取令牌, 以便对`token`方法进行 POST 调用。 下面是如何在[Postman](https://www.getpostman.com/)中执行此操作的示例:

![Postman 标记](media/big-data-cluster-consume-apps/postman_token.png)

此请求的结果将向你发出 JWT `access_token`, 你将需要调用该 URL 才能运行该应用程序。

## <a name="execute-the-app-using-the-restful-web-service"></a>使用 RESTful web 服务执行应用

> [!NOTE]
> 如果需要, 你可以打开在浏览器中运行`swagger` `azdata app describe --name [appname] --version [version]`时返回的的 URL, 该 URL 应类似于`https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`。 你将必须使用你用来`azdata login`登录的同一凭据登录。 的`swagger.json`内容可以粘贴到[Swagger 编辑器](https://editor.swagger.io)。 你会看到 web 服务公开了`run`方法。 另请注意顶部显示的基 URL。

你可以使用你喜欢的`run`工具调用方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`), 并传入 POST 请求正文中的参数作为 json。 在此示例中, 我们将使用[Postman](https://www.getpostman.com/)。 在进行调用之前, 需要将设置`Authorization`为`Bearer Token` , 并将其粘贴到前面检索到的标记中。 这会在你的请求上设置标头。 请参阅下面的屏幕截图。

![Postman 运行标头](media/big-data-cluster-consume-apps/postman_run_1.png)

接下来, 在请求正文中, 将参数传递给你要调用的应用, 并将`content-type`设置`application/json`为:

![Postman 运行正文](media/big-data-cluster-consume-apps/postman_run_2.png)

当你发送请求时, 你将获得与运行应用程序`azdata app run`时所做的相同的输出:

![Postman 运行结果](media/big-data-cluster-consume-apps/postman_result.png)

现已通过 web 服务成功调用应用。 你可以按照类似的步骤在你的应用程序中集成此 web 服务。

## <a name="next-steps"></a>后续步骤

还可以在[应用部署示例](https://aka.ms/sql-app-deploy)中查看其他示例。

有关 SQL Server 大数据群集的详细信息, 请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
