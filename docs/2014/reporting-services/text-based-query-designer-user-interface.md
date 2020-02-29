---
title: 基于文本的查询设计器用户界面 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd3dfdb640c0e2c1b225b0b3a54fcc8bc3ebabc5
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177142"
---
# <a name="text-based-query-designer-user-interface"></a>基于文本的查询设计器用户界面
  使用基于文本的查询设计器可以用数据源支持的查询语言来指定查询，还可以运行查询并在运行时查看结果。 您可以指定多个 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句，为自定义数据处理扩展插件指定查询或命令语法，还可以指定指定为表达式的查询。 因为基于文本的查询设计器不会对查询进行预处理，并且能适应任何类型的查询语法，所以成为了众多数据源类型的默认查询设计器工具。

 基于文本的查询设计器将显示工具栏和以下两个窗格：

-   **查询**显示查询文本、表名或存储过程名称。

-   **结果**显示在设计时运行查询的结果。

## <a name="text-based-query-designer-toolbar"></a>基于文本的查询设计器工具栏
 基于文本的查询设计器为所有命令类型都提供一个单一工具栏。 下表列出了该工具栏中的每个按钮及其功能。

|按钮|说明|
|------------|-----------------|
|**编辑为文本**|在基于文本的查询设计器和图形查询设计器之间切换。 并非所有的数据源类型都支持图形查询设计器。|
|**Import**|从文件或报表中导入现有的查询。 仅支持 .sql 和 .rdl 文件类型。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|
|![运行查询](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "运行查询")|运行查询并在“结果”窗格中显示结果集。|
|**命令类型**|选择 **Text**、 **StoredProcedure**或 **TableDirect**。 如果存储过程带有参数，则单击工具栏上的 **“运行”** 时，将出现 **“定义查询参数”** 对话框，您可以根据需要填入值。 请注意，如果存储过程返回多个结果集，则仅使用第一个结果集填充数据集。<br /><br /> 所支持的命令类型因数据源类型而异。 例如，仅 OLE DB 和 ODBC 支持 **TableDirect**。|

### <a name="command-type-text"></a>命令类型 Text
 创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据集时，默认情况下，报表设计器会显示图形查询设计器。 若要切换为基于文本的查询设计器，请单击工具栏上的“编辑为文本”切换按钮****。 基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格。 下图标出了每个窗格。

 ![用于关系数据查询的通用查询设计器](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "用于关系数据查询的通用查询设计器")

 下表介绍了每个窗格的功能。

|窗格|函数|
|----------|--------------|
|查询|显示 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询文本。 使用此窗格可以编写或编辑 [!INCLUDE[tsql](../includes/tsql-md.md)] 查询。|
|结果|显示查询的结果。 若要运行查询，请右键单击任意窗格，然后单击“运行”，或者单击工具栏中的“运行”按钮********。|

#### <a name="example"></a>示例
 以下查询将从 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库的 `Contact` 表中返回姓氏列表：

```
SELECT LastName FROM Person.Person;
```

 您可以对命令类型文本使用任何 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句，包括 `EXEC` 语句。 下面的查询将调用[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]存储过程`uspGetEmployeeManagers` ，并返回标识号为1的员工的命令链。

```
EXEC uspGetEmployeeManagers 1;
```

 单击工具栏上的 **“运行”** 时，将运行 **“查询”** 窗格中的命令，并在 **“结果”** 窗格中显示结果。

### <a name="command-type-storedprocedure"></a>命令类型 StoredProcedure
 选择“Command typeStoredProcedure”时，基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格****。 在“查询”窗格中输入存储过程的名称，然后单击工具栏中的 **“运行”** 按钮。 此时将打开“定义查询参数”对话框。 输入存储过程的参数值。 对于每个存储过程参数，都会创建一个报表参数。

#### <a name="example"></a>示例
 以下查询调用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 存储过程 `uspGetEmployeeManagers`。 您必须在运行查询时，为雇员标识号参数输入值。

```
uspGetEmployeeManagers;
```

### <a name="command-type-tabledirect"></a>命令类型 TableDirect
 选择“Command typeTableDirect”时，基于文本的查询设计器将显示两个窗格：“查询”窗格和“结果”窗格****。 如果输入一个表并单击 **“运行”** 按钮，则将返回该表的所有列。

#### <a name="example"></a>示例
 以下查询将返回 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中的所有客户的结果集。

 `Sales.Customer`

 输入表名称 Sales. Customer 时，它等效于创建[!INCLUDE[tsql](../includes/tsql-md.md)]语句。 `SELECT * FROM Sales.Customer;`

## <a name="see-also"></a>另请参阅
 [报表设计器 SQL Server Data Tools 中的查询设计工具 &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md) [报表嵌入数据集和共享数据集 &#40;报表生成器和 SSRS](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)&#41;SQL Server 的[连接](report-data/sql-server-connection-type-ssrs.md)类型 &#40;ssrs&#41;OLE DB ssrs &#40;[类型](report-data/ole-db-connection-type-ssrs.md)&#41;[Ssrs &#40;Ssrs](report-data/odbc-connection-type-ssrs.md)&#41;[报表嵌入数据集和共享数据集 &#40;报表生成器和 SSRS](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)&#41;[rsreportdesigner.config 配置文件](report-server/rsreportdesigner-configuration-file.md)


