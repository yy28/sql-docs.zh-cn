---
title: 导入数据，通过使用本机查询 (Analysis Services) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c313484b2ee7ff87668cbfdd0b87ed52cdaf98
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523973"
---
# <a name="import-data-by-using-a-native-query"></a>使用本机查询导入数据
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
对于表格 1400年模型中，在 Visual Studio 的 Analysis Services 项目中获取数据体验提供巨大的灵活性，混合应用程序如何在你的数据导入过程中。 本指南介绍了创建与数据源的连接，然后创建本机 SQL 查询以指定数据导入。

若要完成本文中所述的任务，请确保使用最新版本的 SSDT。 如果您使用的 Visual Studio 2017，请确保已下载并安装 2017 年 9 月或更高版本的 Microsoft Analysis Services 项目 VSIX。

[下载并安装 SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[下载 Microsoft Analysis Services 项目 VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>创建数据源的连接
如果还没有到数据源连接，需要创建一个。

1. 在 Visual Studio 中 >**表格模型资源管理器**，右键单击**数据源**，然后单击**新数据源**。
2. 在中**获取数据**，选择数据源类型，并单击**Connect**。 按照连接到数据源所需的任何其他步骤。


## <a name="enter-a-query-as-a-named-expression"></a>输入查询作为命名表达式
1. 在中**表格模型资源管理器**，右键单击**表达式** > **编辑表达式**。
2. 在中**查询编辑器**，单击**查询** > **新查询** > **空白查询**
3. 在编辑栏中，键入
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. 若要创建表，请在**查询**，右键单击查询，并选择**创建新表**。 新表将具有与查询相同的名称。


## <a name="example"></a>示例
此本机查询包括 Dimension.Employee 表在数据源中的所有列在模型中创建一个雇员表。

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![查询编辑器](media/ssas-import-query-example.png)


导入后，在模型中创建名为 Employees 的表。   

![查询编辑器](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>另请参阅  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [模拟](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
