---
title: 使用 SQL Server 大数据群集上的应用程序
titleSuffix: SQL Server big data clusters
description: 使用在 RESTful web service [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (预览版) 上部署的应用程序。
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d65cb2577749a45bccf1383bdf880ce8c5a7a46
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653061"
---
# <a name="consume-an-app-deployed-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-a-restful-web-service"></a>使用使用 RESTful web 服务[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]部署的应用

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何通过 RESTful Web 服务（预览版）使用部署在 SQL Server 2019 大数据群集上的应用。

## <a name="prerequisites"></a>先决条件

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [azdata 命令行工具](deploy-install-azdata.md)
- 使用 [azdata](big-data-cluster-create-apps.md) 或[应用部署扩展](app-deployment-extension.md)部署的应用

## <a name="capabilities"></a>功能

将应用程序部署到[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]后, 可以使用 RESTful web 服务访问和使用该应用程序。 这样就可以从其他应用程序或服务（例如，移动应用或网站）集成该应用。 下表介绍了一些应用程序部署命令，可将其与 **azdata** 配合使用，为应用获取有关 RESTful Web 服务的信息。

|Command |描述 |
|:---|:---|
|`azdata app describe` | 描述应用程序。 |

可以获取有关 `--help` 参数的帮助，如以下示例中所示：

```bash
azdata app describe --help
```

以下部分介绍如何检索应用程序的终结点，以及如何使用 RESTful Web 服务进行应用程序集成。

## <a name="retrieve-the-endpoint"></a>检索终结点

**azdata app describe** 命令提供有关应用的详细信息，包括群集中的终结点。 应用开发人员通常使用此命令通过 swagger 客户端来生成应用，并使用 Web 服务以 RESTful 的方式与应用进行交互。

运行类似于以下示例的命令来描述你的应用程序:

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
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
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

注意输出中的 IP 地址（本例中为 `10.1.1.3`）和端口号 (`30080`)。

获取此信息的另一种方法是在 Azure Data Studio 的服务器上右键单击 "管理", 你将在其中找到列出的服务的终结点。

![广告终结点](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>生成 JWT 访问令牌

若要为已部署的应用访问 RESTful Web 服务，首先必须生成 JWT 访问令牌。 在浏览器中打开以下 URL：`https://[IP]:[PORT]/docs/swagger.json`（使用通过运行上面的 `describe` 命令检索到的 IP 地址和端口）。 你将需要使用你用来`azdata login`登录的同一凭据登录。

将 `swagger.json` 的内容粘贴到 [Swagger 编辑器](https://editor.swagger.io)中，以了解可用的方法：

![API Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

注意 `app` GET 方法以及 `token` POST 方法。 由于适用于应用的身份验证使用 JWT 令牌, 因此你需要使用你喜欢的工具获取令牌, 以便对`token`方法进行 POST 调用。 下面是如何在 [Postman](https://www.getpostman.com/) 中执行此操作的示例：

![Postman 令牌](media/big-data-cluster-consume-apps/postman_token.png)

此请求的结果将向你发出 JWT `access_token`, 你将需要调用该 URL 才能运行该应用程序。

## <a name="execute-the-app-using-the-restful-web-service"></a>使用 RESTful Web 服务执行应用

> [!NOTE]
> 如果需要，可以打开在浏览器中运行 `azdata app describe --name [appname] --version [version]` 时返回的 `swagger` 的 URL，该 URL 应与 `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json` 类似。 必须使用用于 `azdata login` 的同一凭据登录。 可以将 `swagger.json` 的内容粘贴到 [Swagger 编辑器](https://editor.swagger.io)中。 你将看到 Web 服务公开 `run` 方法。 另请注意顶部显示的基 URL。

你可以使用自己喜欢的工具调用 `run` 方法 (`https://[IP]:30778/api/app/[appname]/[version]/run`)，并在 POST 请求正文中传入参数作为 json。 在此示例中, 我们将使用[Postman](https://www.getpostman.com/)。 在进行调用之前，需要将 `Authorization` 设置为 `Bearer Token` 并粘贴之前检索到的令牌。 这将在你的请求中设置标头。 请参阅以下屏幕截图。

![Postman Run 标头](media/big-data-cluster-consume-apps/postman_run_1.png)

接下来，在请求正文中，将参数传递给要调用的应用并将 `content-type` 设置为 `application/json`：

![Postman Run 正文](media/big-data-cluster-consume-apps/postman_run_2.png)

发送请求时，将获得与通过 `azdata app run` 运行应用时相同的输出：

![Postman Run 结果](media/big-data-cluster-consume-apps/postman_result.png)

现在已通过 Web 服务成功调用应用。 可以按照类似的步骤在应用程序中集成此 Web 服务。

## <a name="next-steps"></a>后续步骤

有关其他示例，请参阅[应用部署示例](https://aka.ms/sql-app-deploy)。

有关的详细信息[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], 请参阅[什么[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]是？](big-data-cluster-overview.md)。
