---
title: 在包中使用变量 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
caps.latest.revision: 62
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0cc23cf94eef3998e1079a09be5978e4c594ca9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285413"
---
# <a name="use-variables-in-packages"></a>在包中使用变量
  变量是对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的有效补充，而且使用非常灵活。它们可以在包中的对象之间以及父包和子包之间提供通信。 变量还可以用在表达式和脚本中。  
  
## <a name="user-defined-variables-and-system-variables"></a>用户定义的变量和系统变量  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供系统变量，而且支持用户定义的变量。 在创建新包时，可以将容器或任务添加到包中，也可以创建事件处理程序， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括一组可用于容器的系统变量。 系统变量包含有关包、容器、任务或事件处理程序的非常有用的信息。 例如，在运行时， **MachineName** 系统变量包含运行包的计算机的名称， **StartTime** 变量包含包开始运行的时间。 系统变量是只读的。 有关详细信息，请参阅 [System Variables](system-variables.md)。  
  
 您可以创建用户定义的变量，然后在包中使用这些变量。 在 [!INCLUDE[ssIS](../includes/ssis-md.md)]中，可以通过很多方式使用用户定义的变量：在脚本中；在由优先约束、For 循环容器、派生列转换和有条件拆分转换使用的表达式中；以及在更新属性值的属性表达式中。  
  
 例如，您可以在 For 循环容器的求值条件中使用用户定义的变量。 您还可以将 Foreach 循环容器中的枚举器集合值映射为变量，如果执行 SQL 任务使用参数化的 SQL 语句，您可以将语句的参数映射为变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)。  
  
## <a name="variables-usage-scenarios"></a>变量使用方案  
 变量在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中有多种不同的使用方式。 您会发现，如果不向包中添加用户定义的变量以实现解决方案所要求的灵活性和可管理性，包的开发将无法进行下去。 根据方案的不同，通常还会用到系统变量。  
  
 **属性表达式** ：在设置包和包对象属性的属性表达式中使用变量来提供值。 例如，表达式 `SELECT * FROM @varTableName` 中包含变量 `varTableName` ，该变量可更新“执行 SQL 任务”所运行的 SQL 语句。 表达式 `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" 通过在月份的第一天运行 `varPackageFirst` 变量指定的包而在其他天中运行 `varPackageOther` 变量指定的包，来更新“执行包”任务所运行的包。 有关详细信息，请参阅 [在包中使用属性表达式](expressions/use-property-expressions-in-packages.md)。  
  
 **数据流表达式** ：在派生列转换和有条件拆分转换用于填充列的表达式中使用变量来提供值，或将数据行定向到不同的转换输出中。 例如，表达式 `@varSalutation + LastName`连接 `VarSalutation` 变量和 `LastName` 列中的值。 表达式 `Income < @HighIncome`将 `Income` 列值小于 `HighIncome` 变量值的数据行定向到一个输出。 有关详细信息，请参阅 [派生列转换](data-flow/transformations/derived-column-transformation.md)、[有条件拆分转换](data-flow/transformations/conditional-split-transformation.md)和 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
 **优先约束表达式** ：提供要在优先约束中用来确定受约束的可执行文件是否运行的值。 这些表达式可以和执行结果（成功、失败、完成）一起使用，也可代替执行结果。 例如，如果表达式 `@varMax > @varMin` 的计算结果为 `true`，则运行可执行文件。 有关详细信息，请参阅 [将表达式添加到优先约束](control-flow/precedence-constraints.md)。  
  
 **参数和返回代码** ：为输入参数提供值，或存储输出参数和返回代码的值。 可通过将变量映射到参数和返回值来执行上述操作。 例如，如果将变量 `varProductId` 设置为 23 并运行 SQL 语句 `SELECT * from Production.Product WHERE ProductID = ?`，查询将检索 `ProductID` 为 23 的产品。 有关详细信息，请参阅 [执行 SQL 任务](control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
 **For 循环表达式** ：提供要在 FOR 循环的初始化表达式、求值表达式和赋值表达式中使用的值。 例如，如果变量 `varCount` 为 2， `varMaxCount` 为 10，初始化表达式为 `@varCount`，求值表达式为  `@varCount < @varMaxCount`，赋值表达式为 `@varCount =@varCount +1`，则循环将重复 8 次。 有关详细信息，请参阅 [For Loop Container](control-flow/for-loop-container.md)。  
  
 **父包变量配置** ：将值由父包传递给子包。 子包可通过使用父包变量配置来访问父包中的变量。 例如，如果子包必须与父包使用相同日期，则子包可以定义一个父包变量配置，该配置将指定 GETDATE 函数在父包中设置的变量。 有关详细信息，请参阅 [Execute Package Task](control-flow/execute-package-task.md) 和 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
 **脚本任务和脚本组件** 为脚本任务或脚本组件提供只读和可读/写变量的列表，在脚本内更新读/写变量，然后在该脚本内或该脚本外使用更新的值。 例如，在代码 `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`中，脚本变量 `numberOfCars` 由 `NumberOfCars`变量中的值更新。 有关详细信息，请参阅 [Using Variables in the Script Task](control-flow/script-task.md)。  
  
## <a name="configurations-and-variables"></a>配置和变量  
 若要动态更新变量，可以为变量创建配置，将这些配置部署到包中，然后在部署包时更新配置文件中的变量值。 在运行时，包使用更新后的变量值。 有关详细信息，请参阅 [创建包配置](../../2014/integration-services/create-package-configurations.md)。  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>添加、修改和删除用户定义的变量  
  
-   [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [设置用户定义变量的属性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
