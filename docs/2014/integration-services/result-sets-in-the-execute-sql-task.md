---
title: 中的结果集执行 SQL 任务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8efb049292caecf21f38ef5bc5a7392138bdcf5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056432"
---
# <a name="result-sets-in-the-execute-sql-task"></a>执行 SQL 任务中的结果集
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中，结果集是否返回到执行 SQL 任务取决于该任务使用的 SQL 命令的类型。 例如，SELECT 语句通常返回结果集，而 INSERT 语句通常不返回结果集。  
  
 结果集所包含的内容也因 SQL 命令而异。 例如，SELECT 语句所返回的结果集可包含零行、单行或多行。 但返回计数或总和的 SELECT 语句所返回的结果集仅包含单个行。  
  
 在执行 SQL 任务中使用结果集不只是要了解 SQL 命令是否返回结果集，以及结果集所包含的内容。 还有其他使用要求和准则可帮助您在执行 SQL 任务中成功使用结果集。 本主题的其余部分将介绍这些使用要求和准则：  
  
-   [指定结果集类型](#Result_set_type)  
  
-   [使用结果集填充变量](#Populate_variable_with_result_set)  
  
-   [配置结果集在执行 SQL 任务编辑器](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a> 指定结果集类型  
 执行 SQL 任务支持下列结果集类型：  
  
-   查询不返回结果时使用的 **“无”** 结果集。 例如，该结果集用于在表中添加、更改和删除记录的查询。  
  
-   查询仅返回一行时使用的 **“单行”** 结果集。 例如，该结果集用于返回计数或总和的 SELECT 语句。  
  
-   查询返回多行时使用的 **“完整结果集”** 结果集。 例如，该结果集用于可检索表中所有行的 SELECT 语句。  
  
-   查询返回 XML 格式的结果集时使用的 **“XML”** 结果集。 例如，该结果集用于包含 FOR XML 子句的 SELECT 语句。  
  
 如果“执行 SQL 任务”使用了 **“完整结果集”** 结果集并且查询返回多个行集，则该任务仅返回第一个行集。 如果该行集生成一个错误，则该任务将报告这个错误。 如果其他行集生成错误，则该任务不会报告这些错误。  
  
##  <a name="Populate_variable_with_result_set"></a> 使用结果集填充变量  
 如果结果集类型为单行、行集或 XML，则可以将查询返回的结果集绑定到用户定义的变量。  
  
 如果结果集类型为“单行”  ，则可以使用列名作为结果集名称，将返回结果中的列绑定到一个变量，也可以使用列列表中列的序号位置作为结果集名称。 例如，查询 `SELECT Color FROM Production.Product WHERE ProductID = ?` 的结果集名称可以是 **Color** 或 **0**。 如果查询返回多个列，而您要访问所有列中的值，则必须将每列绑定到一个不同的变量。 如果使用数字作为结果集名称，将列映射到变量，则数字将反映列在查询的列列表中显示的顺序。 例如，在查询 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`中，对 **Color** 列使用 0，对 **ListPrice** 列使用 1。 使用列名作为结果集名称的功能将依赖于所配置任务要使用的访问接口。 并非所有访问接口都使列名可用。  
  
 某些返回单个值的查询可能不包括列名称。 例如，语句 `SELECT COUNT (*) FROM Production.Product` 不返回列名称。 可以使用序数位置 0 作为结果名称来访问返回结果。 要按列名称访问返回结果，则查询必须包括 AS \<别名> 子句来提供列名称。 语句 `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`提供 **CountOfProduct** 列。 然后可以使用 **CountOfProduct** 列名称或序数位置 0 来访问返回结果列。  
  
 如果结果集类型为“完整结果集”  或 **XML**，则必须使用 0 作为结果集名称。  
  
 当您将一个变量映射到结果集类型为“单行”  的结果集时，该变量的数据类型必须与该结果集包含的列的数据类型兼容。 例如，如果结果集包含 `String` 数据类型的列，则它不能映射到 numeric 数据类型的变量。 当您将设置**TypeConversionMode**属性设置为`Allowed`、 执行 SQL 任务将尝试将输出参数和查询结果的变量的类型的数据的结果分配给。  
  
 XML 结果集只能映射到数据类型为 `String` 或 `Object` 的变量。 如果该变量的数据类型为 `String`，则“执行 SQL 任务”返回一个字符串，并且 XML 源可以使用 XML 数据。 如果该变量的数据类型为 `Object`，则执行 SQL 任务返回一个文档对象模型 (DOM) 对象。  
  
 一个**完整结果集**必须映射到的变量`Object`数据类型。 返回结果是一个行集对象。 可以使用 Foreach 循环容器将存储在对象变量中的表行值提取到包变量中，然后使用脚本任务将存储在包变量中的数据写入文件。 有关如何使用 Foreach 循环容器和脚本任务执行该操作的演示，请参阅 msftisprodsamples.codeplex.com 上的 CodePlex 示例： [执行 SQL 参数和结果集](https://go.microsoft.com/fwlink/?LinkId=157863)。  
  
 下表总结了可以映射到结果集的变量数据类型。  
  
|结果集类型|变量的数据类型|对象的类型|  
|---------------------|---------------------------|--------------------|  
|“单行”|与结果集中的类型列兼容的任意类型。|不适用|  
|“完整结果集”|`Object`|如果任务使用本机连接管理器（包括 ADO、OLE DB、Excel 和 ODBC 连接管理器），则返回的对象为 ADO `Recordset`。<br /><br /> 如果任务使用托管连接管理器（如 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器），则返回的对象为 `System.Data.DataSet`。<br /><br /> 您可以使用脚本任务访问 `System.Data.DataSet` 对象，如下面的示例中所示。<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|如果任务使用本机连接管理器（包括 ADO、OLE DB、Excel 和 ODBC 连接管理器），则返回的对象为 `MSXML6.IXMLDOMDocument`。<br /><br /> 如果任务使用托管的连接管理器中，如[!INCLUDE[vstecado](../includes/vstecado-md.md)]连接管理器，返回的对象是`System.Xml.XmlDocument`。|  
  
 您可在执行 SQL 任务作用域或包作用域内定义变量。 如果变量的作用域为包，则结果集可用于包中的其他任务和容器，并可用于执行包或执行 DTS 2000 包任务所运行的所有包。  
  
 如果将变量映射到“单行”  结果集，则在满足以下条件时，SQL 语句返回的非字符串值将转换为字符串：  
  
-   **TypeConversionMode** 属性设置为 true。 在属性窗口中或通过使用“执行 SQL 任务编辑器”  设置属性值。  
  
-   转换不会导致数据截断。  
  
 有关将结果集加载到变量的信息，请参阅 [在执行 SQL 任务中将结果集映射到变量](control-flow/execute-sql-task.md)。  
  
##  <a name="Configure_result_sets"></a> 中配置结果集执行 SQL 任务  
 有关可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中设置的结果集的属性的详细信息，请单击下列主题：  
  
-   [执行 SQL 任务编辑器&#40;结果集页&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [在执行 SQL 任务中将结果集映射到变量](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>相关内容  
  
-   msftisprodsamples.codeplex.com 上的 CodePlex 示例 [Execute SQL Parameters and Result Sets](https://go.microsoft.com/fwlink/?LinkId=157863)（执行 SQL 参数和结果集）  
  
  
