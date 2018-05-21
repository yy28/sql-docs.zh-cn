---
title: 快速访问见解和 SQL 操作 Studio （预览版） 中的常见任务 |Microsoft 文档
description: 了解如何在 SQL 操作 Studio （预览版） 中显示见解的小组件。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8ed47935a863a14d68385c540ce68d0e75e99799
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>中的仪表板 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

若要查看仪表板、 右键单击服务器或数据库，并选择**管理**。

![示例仪表板](media/dashboards/sample-dashboard.png)

**服务器属性**包含的属性的服务器，包括版本、 版本、 计算机名称和 OS 版本。

**任务**包含 commons 任务，例如还原和新查询。

**搜索数据库**轻松查找存储在服务器上，包括表的现有数据库。

**备份状态**轻松查找现有数据库的备份状态。

## <a name="configuring-insight-widgets"></a>配置见解小组件
强烈建议你遵循本教程设置你的仪表板，可以找到[此处](tutorial-build-custom-insight-sql-server.md)。

此外，请确保要签出[配置见解小组件操作指南]()。

后学习本教程中，继续阅读以了解详细信息不在本教程中介绍的特定小组件。

## <a name="insight-detail"></a>了解详细信息
了解详细信息浮出控件提供了相关的见解小组件的更多详细的信息。 
- 见解小组件呈现具有计数、 折线图、 图表等一览的摘要视图。 
- 了解详细信息弹出提供"钻取"的详细信息，列出高级见解小组件中列出每个项的更深入数据见解。 
  - 详细信息浮出控件内容被定义的主要的小组件查询到单独的 SQL 查询。 

没有任何组要求为了解详细信息查询，但的布局是标准。
- 该视图的上半始终是 2 列的"摘要"视图。 要使用的列定义的 JSON 配置的"标签"和"value"属性
- 在单击摘要表中的行，底部浮出控件的下半部分将列出的整套该行的列信息。

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
|详细信息|json 对象|||必需的属性来定义其结构中的见解详细信息定义||
|queryFile|string|||了解详细信息 sql 查询文件路径和 package.json 位置相对的文件名||
|标签|json 对象|||必需的属性来定义在摘要列表视图中的每个行项|在将来类似 summaryList 更改此属性的名称|
|图标|string|||指示每个摘要列表视图项向呈现的图标名称。|将提供了支持图标 (tbd) 列表|
|column|string|||指示从查询结果集的摘要列表视图中的第一列的名称|将会在将来将此属性的名称更改为更直观的名称|
|值|string|||指示从查询结果集的摘要列表视图中的第二列的名称。 此列的值用于检查条件和设置每个摘要列表视图项颜色点的颜色|在将来将此属性的名称更改为更直观的内容|
|条件 (condition)|json 对象|||定义列的值的条件检查，并确定每个摘要列表视图项的颜色||
|if|string|始终，等于，notEquals、 greaterThan、 lessThan、 greaterThanOrEqauls、 lessThanOrEquals||条件检查运算符|在将来的属性名称将更改为运算符|
|equals|string|||条件检查值|在将来将此属性名更改为 value|

## <a name="insight-actions"></a>操作见解
使用见解小组件和了解详细信息，你可以轻松地出现一个操作计划来缓解问题或管理。 例如，你将执行的 DBCC CHECKDB 将、 读取错误日志或当数据库处于恢复挂起状态时还原数据库。 也可以是任何你想要执行的操作。

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的见解操作配置，你可以将映射内置的操作，例如还原，或者让你自己的 sql 脚本使用定义的操作。

> 使用 sql 脚本的自定义操作配置正处于开发和它目前尚不可用个人预览版内部版本中。

## <a name="sample-insight-action-definition"></a>示例见解操作定义

```"actions"{}``` 定义见解操作。 操作可以定义通过特定的作用域如```"server"```， ```"database"``` ，依此类推和[!INCLUDE[name-sos](../includes/name-sos-short.md)]将当前的连接上下文信息传递到操作。 

例如，还原操作启动 WideWorldImporters 数据库```"database": "${Database}"```定义指示传递```Database```你查询结果设置为还原操作中的列值。 然后还原操作将启动数据库。 ```"types"``` 是一个 json 数组和数组中可以列出多个操作。 它基本上是将成为上下文菜单上了解详细信息对话框该用户可以单击并执行该操作。 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] "备份"、"restore"、"新建查询"和"新数据库"操作类型为已启用了预览 0.17.1。

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
