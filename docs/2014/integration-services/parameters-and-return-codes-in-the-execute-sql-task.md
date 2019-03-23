---
title: 参数和返回代码中执行 SQL 任务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e09e00b4c5dcaf355b5a7691413ed2f8f972d5a6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389685"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>执行 SQL 任务中的参数和返回代码
  SQL 语句和存储过程常常使用 `input` 参数、`output` 参数和返回代码。 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，执行 SQL 任务支持 `Input`、`Output` 和 `ReturnValue` 参数类型。 应当将 `Input` 类型用于输入参数，将 `Output` 用于输出参数并将 `ReturnValue` 用于返回代码。  
  
> [!NOTE]  
>  只有数据访问接口支持这些参数时，才可在执行 SQL 任务中使用它们。  
  
 SQL 命令（包括查询和存储过程）中的参数被映射到在执行 SQL 任务作用域、父容器或包的作用域内创建的用户定义变量。 变量的值可在设计时设置，也可在运行时动态填充。 还可以将参数映射到系统变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)和[系统变量](system-variables.md)。  
  
 但是，在执行 SQL 任务中使用参数和返回代码不只是要了解该任务支持的参数类型以及如何映射这些参数。 还有其他使用要求和准则可帮助您在执行 SQL 任务中成功使用参数和返回代码。 本主题的其余部分将介绍这些使用要求和准则：  
  
-   [使用参数名称和标记](#Parameter_names_and_markers)  
  
-   [将参数用于日期和时间数据类型](#Date_and_time_data_types)  
  
-   [在 WHERE 子句中使用参数](#WHERE_clauses)  
  
-   [在存储过程中使用参数](#Stored_procedures)  
  
-   [获取返回代码的值](#Return_codes)  
  
-   [配置参数和返回代码中执行 SQL 任务编辑器](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> 使用参数名称和标记  
 执行 SQL 任务使用不同的连接类型时，SQL 命令的语法使用不同的参数标记。 例如，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器类型要求，SQL 命令必须使用格式为 \@varParameter 的参数标记，而 OLE DB 连接类型则要求使用问号 (?) 参数标记。  
  
 在变量与参数之间的映射中可以用作参数名的名称也因连接管理器类型而异。 例如，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器类型使用前缀为 \@ 的用户定义的名称，而 OLE DB 连接管理器类型则要求使用从 0 开始的序数数值作为参数名。  
  
 下表总结了执行 SQL 任务可以使用的连接管理器类型的 SQL 命令要求。  
  
|连接类型|参数标记|参数名称|示例 SQL 命令|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<参数名称>|\@\<参数名称>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 和 OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>在 ADO.NET 和 ADO 连接管理器中使用参数  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 和 ADO 连接管理器对使用参数的 SQL 命令有特定要求：  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器要求 SQL 命令将参数名称用作参数标记。 这意味着变量可以直接映射到参数。 例如，变量 `@varName` 映射到名为 `@parName` 的参数，并向参数 `@parName`提供值。  
  
-   ADO 连接管理器要求 SQL 命令将问号 (?) 用作参数标记。 但是，您可以使用任何用户定义名称（整数值除外）作为参数名称。  
  
 为了向参数提供值，可将变量映射到参数名称。 然后，执行 SQL 任务使用参数列表中参数名称的序数值来将值从变量加载到参数。  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>在 EXCEL、ODBC 和 OLE DB 连接管理器中使用参数  
 EXCEL、ODBC 和 OLE DB 连接管理器要求 SQL 命令使用问号 (?) 作为参数标记，并且使用从 0 开始或从 1 开始的数值作为参数名称。 如果执行 SQL 任务使用 ODBC 连接管理器，则映射到查询中的第一个参数的参数名称将为 1；否则该参数将命名为 0。 对于后续参数，参数名称的数值指示参数名称在 SQL 命令中映射到的参数。 例如，名为 3 的参数映射到第三个参数，这是由 SQL 命令中的第三个问号 (?) 来表示的。  
  
 若要向参数提供值，可以将变量映射到参数名称，然后执行 SQL 任务使用参数名称的序数值将值从变量加载到参数。  
  
 连接管理器使用的访问接口不同时，某些 OLE DB 数据类型可能不受支持。 例如，Excel 驱动程序只识别有限的一组数据类型。 有关带有 Excel 驱动程序的 Jet 访问接口的行为的详细信息，请参阅 [Excel Source](data-flow/excel-source.md)。  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>在 OLE DB 连接管理器中使用参数  
 如果执行 SQL 任务使用 OLE DB 连接管理器，则该任务的 BypassPrepare 属性可用。 如果执行 SQL 任务使用带有参数的 SQL 语句，则应将此属性设置为 `true`。  
  
 使用 OLE DB 连接管理器时，不能使用参数化的子查询，这是因为执行 SQL 任务不能通过 OLE DB 访问接口得到参数信息。 但是，您可以使用表达式将参数值串联到查询字符串中，并设置该任务的 SqlStatementSource 属性。  
  
##  <a name="Date_and_time_data_types"></a> 日期和时间数据类型中使用参数  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>在 ADO.NET 和 ADO 连接管理器中使用日期和时间参数  
 读取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 类型 `time` 和 `datetimeoffset` 的数据时，使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 或 ADO 连接管理器的执行 SQL 任务有以下附加要求：  
  
-   有关`time`数据，[!INCLUDE[vstecado](../includes/vstecado-md.md)]连接管理器要求此数据存储在其参数类型的参数`Input`或`Output`，并且数据类型为`string`。  
  
-   对于 `datetimeoffset` 数据，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接管理器要求此数据存储在下列参数之一中：  
  
    -   参数类型为 `Input` 并且数据类型为 `string` 的参数。  
  
    -   参数类型为 `Output` 或 `ReturnValue` 并且数据类型为 `datetimeoffset`、`string` 或 `datetime2` 的参数。 如果选择数据类型为 `string` 或 `datetime2` 的参数，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 会将数据转换为 string 或 datetime2。  
  
-   ADO 连接管理器要求 `time` 或 `datetimeoffset` 数据存储在参数类型为 `Input` 或 `Output` 并且数据类型为 `adVarWchar` 的参数中。  
  
 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>在 OLE DB 连接管理器中使用日期和时间参数  
 使用 OLE DB 连接管理器时，执行 SQL 任务对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型为 `date`、`time`、`datetime`、`datetime2` 和 `datetimeoffset` 的数据有特定的存储要求。 您必须用下列参数类型之一来存储此数据：  
  
-   NVARCHAR 数据类型的输入参数。  
  
-   具有相应数据类型的输出参数，如下表中所示。  
  
    |`Output` 参数类型|Date 数据类型|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`， `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 如果数据未存储在相应的输入或输出参数中，包将失败。  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>在 ODBC 连接管理器中使用日期和时间参数  
 使用 ODBC 连接管理器时，执行 SQL 任务对于带有以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据类型之一的数据具有特定的存储要求：`date`、`time`、`datetime`、`datetime2` 或 `datetimeoffset`。 您必须用下列参数类型之一来存储此数据：  
  
-   SQL_WVARCHAR 数据类型的 `input` 参数  
  
-   具有适当数据类型的 `output` 参数，如下表中所示。  
  
    |`Output` 参数类型|Date 数据类型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -或-<br /><br /> SQL_TIMESTAMP|`datetime`， `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 如果数据未存储在相应的输入或输出参数中，包将失败。  
  
##  <a name="WHERE_clauses"></a> 使用参数在 WHERE 子句  
 SELECT、INSERT、UPDATE 和 DELETE 命令经常包含 WHERE 子句以指定筛选器，这些筛选器定义源表中的每行要用于 SQL 命令所必须满足的条件。 参数在 WHERE 子句中提供筛选值。  
  
 可以使用参数标记来动态提供参数值。 可以在 SQL 语句中使用哪些参数标记和参数名称的规则取决于执行 SQL 所使用的连接管理器的类型。  
  
 下表按连接管理器类型列出了 SELECT 命令的示例。 INSERT、UPDATE 和 DELETE 语句相似。 示例使用 SELECT 返回 **的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 表中 **ProductID** 大于且小于由两个参数指定的值的产品。  
  
|连接类型|SELECT 语法|  
|---------------------|-------------------|  
|EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 这些示例要求使用具有以下名称的参数：  
  
-   EXCEL 和 OLED DB 连接管理器使用参数名称 0 和 1。 ODBC 连接类型使用 1 和 2。  
  
-   ADO 连接类型可以使用任何两个参数名称，例如 Param1 和 Param2，但是这两个参数必须按其在参数列表中的序数位置进行映射。  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 连接类型使用参数名 \@parmMinProductID 和 \@parmMaxProductID。  
  
##  <a name="Stored_procedures"></a> 使用参数的存储过程  
 运行存储过程的 SQL 命令也可以使用参数映射。 与参数化查询的规则一样，参数标记和参数名称的使用规则取决于执行 SQL 所使用的连接管理器的类型。  
  
 下表按连接管理器类型列出了 EXEC 命令的示例。 示例运行 **中的** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]存储过程。 使用存储的过程`@StartProductID`并`@CheckDate``input`参数。  
  
|连接类型|EXEC 语法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> 有关 ODBC 调用语法的详细信息，请参阅 MSDN Library 中的 ODBC 程序员参考的 [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462)（过程参数）主题。|  
|ADO|如果 IsQueryStoredProcedure 设置为`False`， `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> 如果 IsQueryStoredProcedure 设置为`True`， `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|如果 IsQueryStoredProcedure 设置为`False`， `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> 如果 IsQueryStoredProcedure 设置为`True`， `uspGetBillOfMaterials`|  
  
 若要使用输出参数，则语法要求在每个参数标记后跟 OUTPUT 关键字。 例如，以下 output 参数语法是正确的： `EXEC myStoredProcedure ? OUTPUT`。  
  
 有关在 Transact-SQL 存储过程中使用输入和输出参数的详细信息，请参阅 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)。  
  
##  <a name="Return_codes"></a> 获取返回代码的值  
 存储过程可以返回一个整数值（称为“返回代码”），以指示过程的执行状态。 若要在执行 SQL 任务中实现返回代码，需要使用 `ReturnValue` 类型的参数。  
  
 下表按连接类型列出了实现返回代码的某些 EXEC 命令示例。 所有示例均使用 `input` 参数。 有关如何使用参数标记和参数名称的规则是相同的所有参数类型-`Input`， `Output`，和`ReturnValue`。  
  
 某些语法不支持参数文字。 在此情况下，必须通过使用变量来提供参数值。  
  
|连接类型|EXEC 语法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> 有关 ODBC 调用语法的详细信息，请参阅 MSDN Library 中的 ODBC 程序员参考的 [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462)（过程参数）主题。|  
|ADO|如果 IsQueryStoreProcedure 设置为`False`， `EXEC ? = myStoredProcedure 1`<br /><br /> 如果 IsQueryStoreProcedure 设置为`True`， `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|将 IsQueryStoreProcedure 设置为`True`。<br /><br /> `myStoredProcedure`|  
  
 如上表中语法所示，执行 SQL 任务使用 **“直接输入”** 源类型来运行存储过程。 执行 SQL 任务还可以使用 **“文件连接”** 源类型来运行存储过程。 无论执行 SQL 任务是使用**直接输入**或**文件连接**源类型，请使用参数的`ReturnValue`类型来实现返回代码。 有关如何配置执行 SQL 任务运行的 SQL 语句的源类型的详细信息，请参阅[执行 SQL 任务编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)。  
  
 有关在 Transact-SQL 存储过程中使用返回代码的详细信息，请参阅 [RETURN (Transact-SQL)](/sql/t-sql/language-elements/return-transact-sql)。  
  
##  <a name="Configure_parameters_and_return_codes"></a> 配置参数和返回代码中的执行 SQL 任务  
 有关可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中设置的参数和返回代码的属性的详细信息，请单击以下主题：  
  
-   [执行 SQL 任务编辑器&#40;参数映射页&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [设置任务或容器的属性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>相关内容  
  
-   blogs.msdn.com 上的博客项 [Stored procedures with output parameters](https://go.microsoft.com/fwlink/?LinkId=157786)（无输出参数的存储过程）  
  
-   msftisprodsamples.codeplex.com 上的 CodePlex 示例 [Execute SQL Parameters and Result Sets](https://go.microsoft.com/fwlink/?LinkId=157863)（执行 SQL 参数和结果集）  
  
## <a name="see-also"></a>请参阅  
 [执行 SQL 任务](control-flow/execute-sql-task.md)   
 [执行 SQL 任务中的结果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
