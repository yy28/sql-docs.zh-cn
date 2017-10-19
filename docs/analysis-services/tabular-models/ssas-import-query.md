---
title: "通过使用本机查询 (Analysis Services) 导入数据 |Microsoft 文档"
ms.custom: 
ms.date: 10/02/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 8888951d9fca0013015105998200b3ee9364855d
ms.contentlocale: zh-cn
ms.lasthandoff: 10/11/2017

---
# <a name="import-data-by-using-a-native-query"></a>使用本机查询导入数据

对于表格 1400年模型中，Visual Studio 的 Analysis Services 项目中的新获取数据体验提供巨大的灵活性，可以混合应用程序如何在你的数据导入过程中。 本指南介绍了创建到数据源的连接，然后创建本机 SQL 查询，以便指定数据导入。

若要完成本文中所述的任务，请确保使用最新版本的 SSDT。 如果你使用 Visual Studio 2017，请确保你已下载并安装年 9 月 2017年或更高版本的 Microsoft Analysis Services 项目 VSIX。

[下载并安装 SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[下载 Microsoft Analysis Services 项目 VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>创建数据源连接
如果你还没有连接分配到你的数据源，你需要创建一个。

1. Visual Studio 中 >**表格模型资源管理器**，右键单击**数据源**，然后单击**新数据源**。
2. 在**获取数据**，选择数据源类型，，然后单击**连接**。 按照以下任何连接到你的数据源所需的附加步骤。


## <a name="enter-a-query-as-a-named-expression"></a>输入作为命名表达式的查询
1. 在**表格模型资源管理器**，右键单击**表达式** > **编辑表达式**。
2. 在**查询编辑器**，单击**查询** > **新查询** > **空查询**
3. 在公式栏中，键入
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM …")
    ```
4. 若要在创建一个表，**查询**，右键单击查询，，然后选择**创建新表**。 新表将具有与查询相同的名称。


## <a name="example"></a>示例
此本机查询中包括 Dimension.Employee 表在数据源中的所有列的模型创建员工表。

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![查询编辑器](media/ssas-import-query-example.png)


导入之后，在模型中创建名为 Employees 表。   

![查询编辑器](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>另请参阅  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [模拟](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  

