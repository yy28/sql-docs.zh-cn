---
title: 扩展性 API
titleSuffix: Azure Data Studio
description: 了解 Azure Data Studio 扩展性 Api
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a8177492de46c92577eb98e79ece42e77ba947b
ms.sourcegitcommit: ca9b5cb6bccfdba4cdbe1697adf5c673b4713d6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2019
ms.locfileid: "56407607"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 扩展性 Api

[!INCLUDE[name-sos](../includes/name-sos.md)] 提供的 API，扩展可以使用与 Azure Data Studio，对象资源管理器等的其他部分进行交互。 这些 Api 是可从[ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts)文件，如下所述。

## <a name="connection-management"></a>连接管理
`sqlops.connection`

### <a name="top-level-functions"></a>顶级函数

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` 获取基于活动的编辑器或对象资源管理器所选内容的当前连接。

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` 获取用户的所有连接处于活动状态的列表。 如果没有此类连接，则返回一个空列表。

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` 获取一个字典，其中包含与连接关联的凭据。 否则将下面的选项字典的一部分返回这些`sqlops.connection.Connection`对象却获取去除了从该对象。 

### `Connection`
- `options: { [name: string]: string }` 连接选项的字典
- `providerName: string` 连接提供程序的名称 （例如"MSSQL")
- `connectionId: string` 连接的唯一标识符

### <a name="example-code"></a>示例代码
```
> let connection = sqlops.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>“对象资源管理器”

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>顶级函数
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 获取对应于给定的连接和路径的对象资源管理器节点。 如果未不指定任何路径，它将返回给定连接的顶级节点。 如果没有节点在给定的路径，它返回`undefined`。 注意：`nodePath`对象生成的 SQL 工具服务后端，并且难以手动构造。 未来 API 改进将允许你获取基于元数据提供有关该节点，例如名称、 类型和架构的节点。

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 获取所有活动的对象资源管理器连接节点。

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 查找所有匹配的给定元数据的对象资源管理器节点。 `schema`， `database`，并`parentObjectNames`参数都应为`undefined`时它们不适用。 `parentObjectNames` 是从最高到最低级别，在对象资源管理器，所需的对象处于非数据库父对象的列表。 例如，当使用连接 ID 搜索的列"column1"表"schema1.table1"和数据库"database1"属于`connectionId`，调用`findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`。 另请参阅[的 Azure Data Studio 默认情况下支持的类型列表](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API)此 API 调用。

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` 该节点下存在的连接的 id

- `nodePath: string` 用于调用的节点路径`getNode`函数。

- `nodeType: string` 一个表示节点的类型的字符串

- `nodeSubType: string` 一个字符串，表示节点的子类型

- `nodeStatus: string` 一个字符串，表示节点的状态

- `label: string` 在对象资源管理器中显示该节点作为它的标签

- `isLeaf: boolean` 节点是否是叶节点，因此没有任何子级

- `metadata: sqlops.ObjectMetadata` 描述此节点表示的对象的元数据

- `errorMessage: string` 显示节点是否处于错误状态消息

- `isExpanded(): Thenable<boolean>` 节点是否是当前在对象资源管理器中展开

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` 设置该节点是展开还是折叠。 如果状态设置为 None，则该节点将不会更改。

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` 设置是否选择的节点。 如果`clearOtherSelections`是 true，则清除所有其他选择时做出新选择。 如果为 false，将保留任何现有的所选内容。 `clearOtherSelections` 默认值为 true 时`selected`为 true; false 时`selected`为 false。

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 获取所有子节点的节点。 如果没有子级，则返回一个空列表。

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 获取此节点的父节点。 如果没有父级，返回未定义。

### <a name="example-code"></a>示例代码

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>建议的 Api

我们添加了建议的 Api，允许在要自定义用户界面显示在对话框、 向导和文档选项卡，以及其他功能的扩展。 请参阅[建议的 API 类型文件](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts)对于更多文档，但请注意，这些 API 会有变动情况下，在任何时间。 有关如何使用这些 Api 的某些示例可在["sql 服务"示例扩展](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)。


