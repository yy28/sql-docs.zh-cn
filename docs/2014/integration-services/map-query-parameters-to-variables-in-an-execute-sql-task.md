---
title: 将查询参数映射到变量中执行 SQL 任务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cc38f51ef997ea2100e356573af46c3d29aafd66
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388927"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>在执行 SQL 任务中将查询参数映射到变量

  本主题介绍如何在执行 SQL 任务中使用参数化 SQL 语句以及在 SQL 语句的变量和参数之间创建映射。  
  
 若要了解用于不同连接类型的执行 SQL 任务、参数标记和参数名称的详细信息，请参阅 [执行 SQL 任务](control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>将查询参数映射到变量  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  如果该包尚未包括执行 SQL 任务，则向该包的控制流中添加一个此类任务。 有关详细信息，请参阅[添加或删除任务或容器中控制流](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  双击执行 SQL 任务。  
  
6.  以下列方式之一提供参数化 SQL 命令：  
  
    -   在 SQLStatement 属性中使用直接输入并键入 SQL 命令。  
  
    -   使用直接输入，单击 **“生成查询”**，然后使用查询生成器提供的图形工具创建 SQL 命令。  
  
    -   使用文件连接，然后引用包含该 SQL 命令的文件。  
  
    -   使用变量，然后引用包含该 SQL 命令的变量。  
  
     参数化 SQL 语句中使用的参数标记取决于执行 SQL 任务所使用的连接类型。  
  
    |连接类型|参数标记|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 和 SQLMOBILE|@\<参数名称>|  
    |ODBC|?|  
    |EXCEL 和 OLE DB|?|  
  
     下表按连接管理器类型列出了 SELECT 命令的示例。 参数在 WHERE 子句中提供筛选值。 示例使用 SELECT 返回 **的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 表中 **ProductID** 大于且小于由两个参数指定的值的产品。  
  
    |连接类型|SELECT 语法|  
    |---------------------|-------------------|  
    |EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     有关在存储过程中使用参数的示例，请参阅 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
7.  单击 **“参数映射”**。  
  
8.  若要添加参数映射，请单击 **“添加”**。  
  
9. 在 **“参数名称”** 框中提供名称。  
  
     所使用的参数名称取决于执行 SQL 任务所使用的连接类型。  
  
    |连接类型|“参数名称”|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, …|  
    |ADO.NET 和 SQLMOBILE|@\<参数名称>|  
    |ODBC|1, 2, 3, …|  
    |EXCEL 和 OLE DB|0, 1, 2, 3, …|  
  
10. 从 **“变量名称”** 列表中选择变量。 有关详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
11. 在 **“方向”** 列表中指定该参数是输入、输出还是返回值。  
  
12. 在 **“数据类型”** 列表中，设置该参数的数据类型。  
  
    > [!IMPORTANT]  
    >  参数的数据类型必须与变量的数据类型兼容。  
  
13. 对 SQL 语句中的每个参数重复步骤 8 到 11。  
  
    > [!IMPORTANT]  
    >  参数映射的顺序必须与参数在 SQL 语句中出现的顺序相同。  
  
14. 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [执行 SQL 任务](control-flow/execute-sql-task.md)   
 [参数和返回代码中执行 SQL 任务](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)  
  
  
