---
title: 通过扩展性添加其他功能
titleSuffix: Azure Data Studio
description: 了解如何扩展模型和用于扩展的 Azure Data Studio 功能的重要扩展功能区域
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: ce80ae9ec15fc7e1fdf8c68b595c71b2ee3f0a64
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105043"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>开始使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]扩展性

[!INCLUDE[name-sos](../includes/name-sos.md)] 有几种扩展性机制，以自定义用户体验并使这些自定义项可供整个用户社区。 核心[!INCLUDE[name-sos](../includes/name-sos.md)]平台基于 Visual Studio Code 中，因此 Visual Studio Code 扩展性 Api 的大部分都是可用。 此外，我们提供了其他扩展点进行数据管理特定于活动。

下面是一些关键扩展点：

- Visual Studio Code 扩展性 Api
- 创作工具的 azure Data Studio 扩展
- 管理仪表板选项卡面板组件
- 通过操作体验的见解
- Azure Data Studio 扩展性 Api
- 自定义数据提供程序 Api

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code 扩展性 Api

由于核心[!INCLUDE[name-sos](../includes/name-sos.md)]平台基于 Visual Studio Code、 关于 Visual Studio Code 扩展性 Api 的详细信息，请参阅[扩展插件创作](https://code.visualstudio.com/docs/extensions/overview)并[扩展 API](https://code.visualstudio.com/docs/extensionAPI/overview)Visual Studio Code 网站上的文档。

## <a name="manage-dashboard-tab-panel-contributions"></a>管理仪表板选项卡面板组件

有关详细信息，请参阅[贡献点](#contribution-points)并[上下文变量](#context-variables)。

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 扩展性 Api

有关详细信息，请参阅[扩展性 Api](extensibility-apis.md)。


## <a name="contribution-points"></a>贡献点

本部分介绍在 package.json 扩展清单中定义的各种贡献点。

在 azuredatastudio 内支持 IntelliSense。

## <a name="contributes-dashboard"></a>提供仪表板

参与选项卡、 容器、 见解小组件到仪表板。

![面板](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs 创建仪表板页面内的选项卡部分。 它需要一个对象的数组。  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

而不是指定仪表板容器内联 （在内部 dashboard.tab)。 你可以注册使用 dashboard.containers 的容器。 它接受一个对象的数组。

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

若要引用已注册的容器，请指定容器的 id

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

你可以注册使用 dashboard.insights 的见解。 它类似于[教程：生成自定义见解小组件](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>仪表板的容器类型

目前有四个支持的容器类型：

1. `widgets-container`

    ![小组件容器](media/extensibility/widgets-container.png)

    将容器中显示的小组件的列表。 它是流布局。 它接受小组件的列表。

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![webview 容器](media/extensibility/webview-container.png)

    Web 视图将显示在整个容器。 它需要 web 视图 id 为也是选项卡 ID

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![网格容器](media/extensibility/grid-container.png)

   小组件或将网格布局中显示的 webview 的列表

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![nav 部分](media/extensibility/nav-section.png)

    导航部分将显示在容器中

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>上下文变量

有关在 Visual Studio Code 和 Azure Data Studio 随后的上下文的常规信息，请参阅[扩展性](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)。

在 Azure Data Studio，我们有特定的上下文信息可用于扩展数据库连接。

### <a name="dashboard"></a>面板

在仪表板中，我们提供以下上下文变量：

|上下文变量| description|
|:---|:---|
|`connectionProvider` | 当前连接的提供程序的标识符的字符串。 例如： `connectionProvider == 'MSSQL'` 的用户。|
|`serverName`|当前连接的服务器名称的字符串。 例如： `serverName == 'localhost'` 的用户。|
|`databaseName` | 当前连接的数据库名称的字符串。 例如： `databaseName == 'master'` 的用户。|
|`connection` | 当前连接 (IConnectionProfile) 的完整的连接配置文件对象|
|`dashboardContext` | 在目前的仪表板的页面的上下文字符串。 数据库或者服务器。 例如： `dashboardContext == 'database'`|
