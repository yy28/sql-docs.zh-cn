---
title: 使用大数据群集上的应用程序
titleSuffix: SQL Server 2019 big data clusters
description: 使用 SQL Server 2019 大数据群集使用 RESTful web 服务 （预览版） 上部署的应用程序。
author: jeroenterheerdt
ms.author: jterh
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.reviewer: rothja
ms.openlocfilehash: a9ef02cae7899a1deb5ce6d84b10dac2297b9d2f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389955"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>使用 SQL Server 使用 RESTful web 服务的大数据群集上部署的应用

本文介绍如何使用 SQL Server 2019 大数据群集使用 RESTful web 服务 （预览版） 上部署的应用。

## <a name="prerequisites"></a>先决条件

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [mssqlctl 命令行实用程序](deploy-install-mssqlctl.md)
- 部署使用的应用[ `mssqlctl` ](big-data-cluster-create-apps.md)或[应用将部署扩展](app-deployment-extension.md)

## <a name="capabilities"></a>功能

部署到 SQL Server 2019 大数据群集 （预览版） 的应用程序后，可以访问和使用该应用程序使用 RESTful web 服务。 这使该应用从其他应用程序或服务 （例如，移动应用或网站） 的集成。 下表描述了可用于应用程序部署命令**mssqlctl**以获取有关你的应用的 RESTful web 服务的信息。

|Command |Description |
|:---|:---|
|`mssqlctl app describe` | 介绍应用程序。 |

可以获取帮助`--help`参数，如以下示例所示：

```bash
mssqlctl app describe --help
```

以下部分介绍如何检索应用程序的终结点以及如何使用 RESTful web 服务的应用程序集成。

## <a name="retrieve-the-endpoint"></a>检索的终结点

**Mssqlctl 应用描述**命令提供了有关应用程序包括在群集中的终结点的详细的信息。 这通常用于由应用开发人员生成的应用程序使用 swagger 客户端和使用 web 服务与应用交互以 RESTful 方式。

通过运行类似以下的命令描述您的应用程序：

```bash
mssqlctl app describe --name addpy --version v1
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

记下 IP 地址 (`10.1.1.3`在此示例中) 和端口号 (`30777`) 在输出中。

## <a name="generate-a-jwt-access-token"></a>生成一个 JWT 访问令牌

若要访问已部署的应用的 RESTful web 服务首先需要生成一个 JWT 访问令牌。 在你的浏览器中打开以下 URL:`https://[IP]:[PORT]/api/docs/swagger.json`使用的 IP 地址和端口运行检索`describe`上述命令。 必须能够使用所用的同一凭据进行登录`mssqlctl login`。

粘贴的内容`swagger.json`成[Swagger 编辑器](https://editor.swagger.io)可了解哪些方法：

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

请注意`app`GET 方法并将`token`POST 方法。 由于应用的身份验证使用 JWT 令牌将需要获取令牌，我使用你喜欢的工具进行 POST 调用以`token`方法。 下面是如何做到这一点的示例[Postman](https://www.getpostman.com/):

![Postman 令牌](media/big-data-cluster-consume-apps/postman_token.png)

此请求的结果将为您提供 JWT `access_token`，这将需要调用要运行该应用程序的 URL。

## <a name="execute-the-app-using-the-restful-web-service"></a>执行应用程序使用 RESTful web 服务

> [!NOTE]
> 如果你想，您可以打开的 URL`swagger`在运行时返回`mssqlctl app describe --name [appname] --version [version]`在浏览器中，这应类似于`https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`。 必须能够使用所用的同一凭据进行登录`mssqlctl login`。 内容`swagger.json`您可以将其粘贴到[Swagger 编辑器](https://editor.swagger.io)。 你将看到该 web 服务公开了`run`方法。 另请注意在顶部显示的基 URL。

可以使用你喜欢的工具来调用`run`方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`)，并传入 POST 请求以 json 形式的正文中的参数。 在此示例中我们将使用[Postman](https://www.getpostman.com/)。 在调用前，你将需要设置`Authorization`到`Bearer Token`并粘贴在前面检索到的令牌。 这会将设置你的请求标头。 请参见以下屏幕截图。

![Postman 运行标头](media/big-data-cluster-consume-apps/postman_run_1.png)

接下来，在请求正文中，将参数传递给正在调用和设置的应用`content-type`到`application/json`:

![Postman 运行正文](media/big-data-cluster-consume-apps/postman_run_2.png)

如果发送请求，将会收到与相同的输出时运行应用程序一样`mssqlctl app run`:

![Postman 运行结果](media/big-data-cluster-consume-apps/postman_result.png)

已成功现在调用通过 web 服务应用程序。 可以遵循类似的步骤来将此应用程序中的 web 服务集成。

## <a name="next-steps"></a>后续步骤

您还可以查看其他示例位于[应用程序部署示例](https://aka.ms/sql-app-deploy)。

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。
