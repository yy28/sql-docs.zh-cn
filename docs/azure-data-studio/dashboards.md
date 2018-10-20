---
title: 快速访问 insights 和 Azure Data Studio 中的常见任务 |Microsoft Docs
description: 了解有关在 Azure Data Studio 中显示见解深刻的小组件。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: b163d110353d07811f0feb991772c90053651659
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356190"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>中的仪表板 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

若要查看的仪表板中，右键单击服务器或数据库，并选择**管理**。

![示例仪表板](media/dashboards/sample-dashboard.png)

**服务器属性**包含服务器，包括版本、 版本、 计算机名称和 OS 版本的属性。

**任务**包含 commons 任务，例如还原和新查询。

**搜索数据库**轻松地查找存储在服务器上，包括表上的现有数据库。

**备份状态**轻松地查找现有数据库的备份状态。

## <a name="configuring-insight-widgets"></a>配置见解小组件
强烈建议您按照设置你的仪表板，可找到教程[此处](tutorial-build-custom-insight-sql-server.md)。

此外，请确保要签出[操作方法上配置见解小组件]()。

后遵循本教程中，继续阅读以了解有关本教程中未涵盖的特定小组件的详细信息。

## <a name="insight-detail"></a>了解详细信息
了解详细信息浮出控件提供了相关的见解小组件的更多详细的信息。 
- 见解小组件用于呈现使用计数、 行、 图表等一眼摘要视图。 
- 了解详细信息浮出控件提供了"钻取"的详细信息，列出高级见解小组件中列出的各项的更深入的数据见解。 
  - 详细信息浮出控件内容使用单独的 SQL 查询与主小组件的查询定义。 

了解详细信息查询中，没有组要求，但标准布局。
- 视图的上半部分是始终 2 列"的摘要"视图。 要使用的列定义的 JSON 配置的"标签"和"value"属性
- 单击摘要表中的行，在底部浮出控件的下半部分将列出的完整集的行的列信息。

### <a name="insight-detail-configuration-in-packagejson"></a>在 package.json 中了解详细信息配置

浮出控件的示例了解详细信息的配置
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```
|属性|type|值|默认值|description|comment|
|:---|:---|:---|:---|:---|:---|
|详细信息|json 对象|||若要定义其结构中的了解详细信息定义的必需属性||
|queryFile|string|||了解详细信息 sql 查询文件路径和文件名相对于 package.json 位置||
|标签|json 对象|||若要在摘要列表视图中定义每个行项的必需属性|在将来的此属性以更改，例如 summaryList 名称|
|图标|string|||指示呈现到每个摘要列表视图项的图标名称。|将记录 (tbd) 受支持的图标列表|
|column|string|||指示从查询结果集的摘要列表视图中的第一列的名称|在将来将此属性的名称更改为更直观的名称|
|值|string|||指示从查询结果集的摘要列表视图中的第二个列的名称。 此列的值用于检查条件并设置每个摘要列表视图项颜色圆点的颜色|在将来将此属性的名称更改为更直观的内容|
|条件 (condition)|json 对象|||定义列的值的条件检查，并确定每个摘要列表视图项的颜色||
|if|string|始终，equals、 notEquals、 greaterThan、 lessThan、 greaterThanOrEqauls、 lessThanOrEquals||条件检查运算符|在将来的属性名称将更改为运算符|
|equals|string|||条件检查值|在将来将此属性名称更改为 value|

## <a name="insight-actions"></a>操作见解
使用见解小组件和了解详细信息，您可以轻松地采用一个操作计划来缓解问题或管理。 例如，将考虑执行的 DBCC CHECKDB、 读取错误日志或还原数据库时数据库处于恢复挂起状态。 也可以是任何您想要执行的操作。

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的见解操作配置，您可以将映射内置的操作，例如还原，或将你自己使用的 sql 脚本定义的操作。

> 配置的 sql 脚本并使用自定义操作处于开发阶段，尚不可用的专用预览版中。

## <a name="sample-insight-action-definition"></a>示例见解操作定义

```"actions"{}``` 定义的见解操作。 操作可定义通过特定的作用域等```"server"```，```"database"```等和[!INCLUDE[name-sos](../includes/name-sos-short.md)]将当前连接上下文信息传递给该操作。 

例如，还原操作启动 WideWorldImporters 数据库```"database": "${Database}"```定义表示要传递```Database```在查询结果设置为还原操作中列的值。 然后还原操作会启动数据库。 ```"types"``` 是一个 json 数组和数组中可以列出多个操作。 它基本上是将成为一个上下文菜单，该用户可以了解详细信息对话框上单击并执行该操作。 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] 预览 0.17.1 已启用"备份"、"还原"、"新建查询"和"新的数据库"作为操作类型。

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
