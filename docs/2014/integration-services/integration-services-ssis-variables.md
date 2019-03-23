---
title: Integration Services (SSIS) 变量 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b824129d1687dce8471800f79d106328b9ee36f6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388932"
---
# <a name="integration-services-ssis-variables"></a>Integration Services (SSIS) 变量
  变量存储 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包及其容器、任务和事件处理程序在运行时可以使用的值。 脚本任务和脚本组件中的脚本也可以使用变量。 将任务和容器按顺序组织为工作流的优先约束在其约束定义包含表达式时可以使用变量。  
  
 可以将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包中的变量用于下列目的：  
  
-   在运行时更新包元素的属性。 例如，可以动态设置 Foreach 循环容器所允许的并发可执行文件数。  
  
-   包含内存中的查找表。 例如，包可以运行加载带数据值的变量的执行 SQL 任务。  
  
-   加载带数据值的变量，然后使用这些变量指定 WHERE 子句中的搜索条件。 例如，脚本任务中的脚本可以更新执行 SQL 任务中的 Transact-SQL 语句所使用的变量的值。  
  
-   加载带整数的变量，然后使用该值控制包控制流中的循环。 例如，可以在 For 循环容器的计算表达式中使用变量来控制迭代。  
  
-   在运行时填充 Transact-SQL 语句的参数值。 例如，包可以运行执行 SQL 任务，然后使用变量动态设置 Transact-SQL 语句中的参数。  
  
-   生成包含变量值的表达式。 例如，派生列转换可以用变量值乘以列值所得结果来填充列。  
  
## <a name="system-and-user-defined-variables"></a>系统变量和用户定义变量  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支持两种类型的变量：用户定义变量和系统变量。 用户定义变量由包开发人员定义，系统变量由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]定义。 可以创建包所需数量的用户定义变量，但不能另外创建系统变量。  
  
 在执行 SQL 任务用来在 SQL 语句中将变量映射到参数的参数绑定中，可以使用所有变量（系统和用户定义）。 有关详细信息，请参阅 [执行 SQL 任务](control-flow/execute-sql-task.md) 和 [执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
> [!NOTE]  
>  用户定义变量和系统变量的名称是区分大小写的。  
  
 可以为所有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器类型创建用户定义变量，这些容器类型包括包、Foreach 循环容器、For 循环容器、序列容器、任务以及事件处理程序。 用户定义变量是容器中 Variables 集合的成员。  
  
 使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建包时， **设计器** “包资源管理器” **选项卡上的** “变量” [!INCLUDE[ssIS](../includes/ssis-md.md)] 文件夹中可以看到 Variables 集合的成员。 这些文件夹列出了用户定义变量和系统变量。  
  
 可以使用下列方式配置用户定义变量：  
  
-   提供变量的名称和说明。  
  
-   指定变量的命名空间。  
  
-   指示变量是否在其值更改时引发事件。  
  
-   指示变量是只读还是读/写。  
  
-   使用表达式的计算结果设置变量值。  
  
-   在包或包对象（如任务）的范围内创建变量。  
  
-   指定变量的值和数据类型。  
  
 对系统变量唯一可配置的选项是指定变量在更改值时是否引发事件。  
  
 不同的容器类型有一组不同的系统变量可用。 有关包及其元素所使用的系统变量的详细信息，请参阅 [System Variables](system-variables.md)。  
  
 有关变量的实际使用情况的详细信息，请参阅[在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)。  
  
## <a name="variable-properties"></a>变量属性  
 你可通过在“变量”窗口或“属性”窗口中设置以下属性来配置用户定义变量。 某些属性仅在“属性”窗口中提供。  
  
> [!NOTE]  
>  对系统变量唯一可配置的选项是指定变量在更改值时是否引发事件。  
  
 Description  
 指定对变量的描述。  
  
 EvaluateAsExpression  
 当属性设置为`True`，所提供的表达式用于设置变量值。  
  
 表达式  
 指定分配给该变量的表达式。  
  
 “属性”  
 指定变量名称。  
  
 命名空间  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了两个命名空间：User 和 System。 默认情况下，自定义变量位于 **User** 命名空间中，系统变量位于 **System** 命名空间中。 你可以为用户定义变量创建其他命名空间，并可以更改 **User** 命名空间的名称，但不能更改 **System** 命名空间的名称，也不能向 **System** 命名空间添加变量或将系统变量分配给其他命名空间。  
  
 RaiseChangedEvent  
 将此属性设置为 `True` 时，变量值的改变将会引发 `OnVariableValueChanged` 事件。  
  
 ReadOnly  
 将此属性设置为 `False` 时，该变量为读\写变量。  
  
 范围  
 > [!NOTE]  
>  可通过单击“变量”窗口中的“移动变量”来更改此属性设置。  
  
 变量在包的作用域内或者包中的容器、任务或事件处理程序的作用域内创建。 因为包容器位于容器层次结构的顶部，所以包作用域内的变量所起作用类似于全局变量，而且这些变量可由包中所有容器使用。 同样，在 For 循环容器等容器的范围内定义的变量可由 For 循环容器中所有任务或容器使用。  
  
 如果包使用执行包任务运行其他包，则可以使用父包变量配置类型，使在调用的包或执行包任务范围内定义的变量可供被调用的包使用。 有关详细信息，请参阅 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
 IncludeInDebugDump  
 指示调试转储文件中是否包括变量值。  
  
 对于用户定义的变量和系统变量的默认值为**InclueInDebugDump**选项是`true`。  
  
 但是，对于用户定义变量，系统将重置**IncludeInDebugDump**选项设为`false`时满足以下条件：  
  
-   如果**EvaluateAsExpression**变量的属性设置为`true`，系统将重置**IncludeInDebugDump**选项设为`false`。  
  
     若要在调试转储文件中包含的文本作为变量值的表达式，设置**IncludeInDebugDump**选项设为`true`。  
  
-   如果变量数据类型更改为字符串时，系统会重置**IncludeInDebugDump**选项设为`false`。  
  
 时系统将重置**IncludeInDebugDump**选项设为`false`，这可能会覆盖用户选择的值。  
  
 ReplTest1  
 用户定义变量的值可以是文字或表达式。 变量包含设置变量值和值的数据类型的选项。 这两种属性必须兼容：例如，字符串值不能与整数数据类型一起使用。  
  
 如果将变量配置为作为表达式进行计算，则必须提供表达式。 在运行时计算表达式，而该变量将设置为计算结果。 例如，如果变量使用表达式 `DATEPART("month", GETDATE())` ，则变量的值与当前日期月份部分的数字相同。 表达式必须是使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 表达式语法的有效表达式。 表达式和变量一起使用时，表达式可以使用文字以及表达式语法所提供的运算符和函数，但表达式不能引用包中数据流的列。 表达式的最大长度为 4000 个字符。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。  
  
 ValueType  
 > [!NOTE]  
>  此属性值出现在“变量”窗口中的“数据类型”列中。  
  
 指定变量值的数据类型。  
  
## <a name="configuring-variables"></a>配置变量  
 可以通过 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [“变量”窗口](../../2014/integration-services/variables-window.md)。  
  
 若要了解变量属性的详细信息，以及关于以编程方式设置这些属性的详细信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.Variable>。  
  
## <a name="related-tasks"></a>Related Tasks  
 [添加、删除、更改包中用户定义变量的作用域](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [设置用户定义变量的属性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [在子包中使用变量和参数的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [将查询参数映射到数据流组件中的变量](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
