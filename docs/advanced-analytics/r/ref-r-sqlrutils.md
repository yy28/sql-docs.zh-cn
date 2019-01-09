---
title: sqlrutils 帮助程序函数-SQL Server 机器学习服务
description: 使用 R 使用 sqlrutils 函数库在 SQL Server 2016 R Services 和 SQL Server 2017 机器学习服务中的生成包含 R 脚本的存储的过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6bcf721158aec7c7aaddd36d0965349582e155bd
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596868"
---
# <a name="sqlrutils-r-library-in-sql-server"></a>sqlrutils （SQL Server 中的 R 库）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**sqlrutils** 包为 R 用户提供一种机制，将他们的 R 脚本置于 T-SQL 存储过程中、向数据库注册该存储过程并从 R 开发环境运行存储过程。 

通过转换 R 代码以在单个存储过程中运行，可更有效地利用 SQL Server R Services，它要求将 R 脚本作为参数嵌入 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 **sqlrutils** 包有助于构建此嵌入的 R 脚本并正确设置相关参数。

 **Sqlrutils** 包执行以下任务：

- 将生成的 T-SQL 脚本保存为 R 数据结构内的字符串
- 可以选择为 T-SQL 脚本生成 .sql 文件，可编辑或运行此文件来创建存储过程
- 从 R 开发环境向 SQL Server 实例注册新创建的存储过程

也可通过传递格式正确的参数并处理结果，从 R 环境执行存储过程。 或者可使用 SQL Server 中的存储过程来支持常见数据库集成方案，例如 ETL、模型定型和大批量评分。

  > [!NOTE]
  > 若打算通过调用 *executeStoredProcedure* 函数从 R 环境运行存储过程，必须使用 ODBC 3.8 提供程序，例如适用于 SQL Server 的 ODBC Driver 13。  
  
## <a name="full-reference-documentation"></a>完整的参考文档

**Sqlrutils**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[单个 sqlrutils 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)发布到下一个位置[R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="functions-list"></a>函数列表

以下部分概述可以从调用的函数**sqlrutils**包开发一个存储的过程，其中包含嵌入的 R 代码。 为每个方法或函数的参数的详细信息，请参阅包的 R 帮助： `help(package="sqlrutils")`

|函数 | Description |
|------|-------------|
|[ExecuteStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/executestoredprocedure)| 执行 SQL 存储过程。|
|[getInputParameters](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/getinputparameters)| 获取对存储过程的输入参数的列表。| 
|[InputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputdata)| 在 SQL Server 中定义将用于 R 数据帧的数据源。 指定 data.frame（在其中存储输入数据）的名称和获取数据的查询或默认值。 仅支持简单的 SELECT 查询。 | 
|[来执行存储过程](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/inputparameter)| 定义将嵌入 T-SQL 脚本的单个输入参数。 必须提供参数名称及其 R 数据类型。| 
|[OutputData](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputdata)| 如果 R 函数返回包含 data.frame 的列表，则会生成所需的中间数据对象。 *OutputData* 对象用于存储从列表获取的单个 data.frame 的名称。| 
|[OutputParameter](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/outputparameter) | 如果 R 函数返回列表，则会生成所需的中间数据对象。 *OutputParameter* 对象存储列表中单个成员的名称和数据类型，假定此成员 **不是** 数据帧。 |
|[registerStoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/registerstoredprocedure) | 向数据库注册存储的过程。|
|[setInputDataQuery](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputdataquery)| 将查询分配给存储过程的输入的数据参数。| 
|[setInputParameterValue](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/setinputparametervalue)| 将值分配给存储过程的输入参数。| 
|[StoredProcedure](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/storedprocedure)| 存储的过程对象。|


## <a name="how-to-use-sqlrutils"></a>如何使用 sqlrutils

**Sqlrutils**库函数必须在具有 SQL Server 机器学习的计算机上运行如果您正在客户端工作站上，设置为 shift 执行转移到 SQL Server 的远程计算上下文。 使用此包的工作流包括以下步骤：

+ 定义存储的过程参数 （输入、 输出，或两者） 
+ 生成并注册存储的过程    
+ 执行该存储过程  

在 R 会话中，加载**sqlrutils**从命令行键入`library(sqlrutils)`。

> [!Note]
> 您可以加载此库不具有 SQL Server （例如，在 R 客户端实例） 如果将计算上下文更改为 SQL Server 并在该计算上下文中执行代码的计算机上。


### <a name="define-stored-procedure-parameters-and-inputs"></a>定义存储的过程参数和输入

`StoredProcedure` 是用于构建存储过程的主构造函数。 此构造函数生成 *SQL Server 存储过程* 对象，并选择性地创建包含查询的文本文件，其中此查询可使用 T-SQL 命令生成存储过程。 

或者， *StoredProcedure* 函数也可向指定的实例和数据库注册存储过程。

+ 使用 `func` 参数指定有效的 R 函数。 该函数使用的所有变量必须在函数中定义或作为输入参数提供。 这些参数最多可包含一个数据帧。

+ R 函数必须返回数据帧、已命名列表或 NULL。 如果该函数返回列表，则列表最多可以包含一个 data.frame。

+ 使用参数 `spName` 指定要创建的存储过程的名称。

+ 可通过使用以下帮助器函数创建的对象，在可选输入和输出参数中传递： `setInputData`、 `setInputParameter`和 `setOutputParameter`。

+  可选择使用 `filePath` 提供要创建的 .sql 文件的路径和名称。 可在 SQL Server 实例上运行此文件，使用 T-SQL 生成存储过程。

+ 若要定义将保存存储过程的服务器和数据库，可使用参数 `dbName` 和  `connectionString`。

+ 若要获取用于创建特定 *StoredProcedure* 对象的 *InputData* 和 *InputParameter* 对象的列表，可调用 `getInputParameters`。 

+ 若要向指定数据库注册存储过程，可使用 `registerStoredProcedure`。

存储过程对象通常没有任何关联数据或值，除非指定了默认值。 执行存储过程之前，不会检索数据。 

### <a name="specify-inputs-and-execute"></a>指定输入和执行

+ 使用 `setInputDataQuery` 将查询分配到 *InputParameter* 对象。 例如，如果已在 R 中创建存储过程对象，可使用 `setInputDataQuery` 将参数传递到 *StoredProcedure* ，以使用所需输入执行存储过程。

+ 使用 `setInputValue` 将特定值分配到存储为 *InputParameter* 对象的参数。 然后将参数对象及其值分配传递到 *StoredProcedure* ，以使用设定值执行存储过程。

+ 使用 `executeStoredProcedure` 执行定义为 *StoredProcedure* 对象的存储过程。 仅当从 R 代码执行存储过程时，调用此函数。 使用 T-SQL 从 SQL Server 运行存储过程时，请勿使用它。

> [!NOTE]
> *executeStoredProcedure* 函数需要 ODBC 3.8 提供程序，例如适用于 SQL Server 的 ODBC Driver 13。  

## <a name="see-also"></a>另请参阅

[如何创建使用 sqlrutils 对存储的过程](how-to-create-a-stored-procedure-using-sqlrutils.md)

