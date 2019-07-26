---
title: 用于 Python 和 R 教程的 Iris 演示数据集
Description: 创建一个包含 Iris 数据集的数据库和一个用于存储模型的表。 此数据集用于演示如何在 SQL Server 存储过程中包装 R 语言或 Python 代码的练习。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9e5fb470e9045060e6cf2423470c2e4e1ee14f30
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469651"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>SQL Server 中的 Python 和 R 教程的 Iris 演示数据 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此练习中, 将创建一个 SQL Server 数据库, 用于存储来自[Iris 花数据集](https://en.wikipedia.org/wiki/Iris_flower_data_set)的数据和基于相同数据的模型。 Iris 数据同时包含在 SQL Server 安装的 R 和 Python 分发版中, 用于 SQL Server 的机器学习教程。 

若要完成此练习, 您应该有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或可以运行 t-sql 查询的其他工具。

使用此数据集的教程和快速入门包括:

+  [起步使用中的存储过程创建、定型和使用 Python 模型 SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>创建数据库

1. 开始 SQL Server Management Studio, 并打开一个新的**查询**窗口。  

2. 为此项目创建一个新数据库, 然后更改**查询**窗口的上下文以使用新的数据库。

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > 如果你不熟悉 SQL Server 或者正在使用自己的服务器, 则常见的错误是登录并开始工作, 而不会发现你在**master**数据库中。 若要确保使用正确的数据库, 请始终使用`USE <database name>`语句 (例如, `use irissql`) 指定上下文。

3. 添加一些空表: 一个用于存储数据, 另一个用于存储定型模型。 **Iris_models**表用于存储在其他练习中生成的序列化模型。

    下面的代码将为定型数据创建表。

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

    > [!TIP] 
    > 如果你不熟悉 t-sql, 则需要记住该`DROP...IF`语句。 当你尝试创建一个表并且一个已存在时, SQL Server 将返回错误:"数据库中已经有一个名为" iris_data "的对象。 避免此类错误的一种方法是在代码中删除任何现有的表或其他对象。

4. 运行以下代码以创建用于存储定型模型的表。 若要在 SQL Server 中保存 Python (或 R) 模型, 必须将其序列化并存储在**varbinary (max)** 类型的列中。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除了模型内容外, 通常还会添加其他有用元数据的列, 例如模型名称、训练日期、源算法和参数、源数据等。 现在, 我们将保持简单, 只使用模型名称。

## <a name="populate-the-table"></a>填充表

可以从 R 或 Python 获取内置的 Iris 数据。 您可以使用 Python 或 R 将数据加载到数据帧中, 然后将其插入到数据库中的表中。 将定型数据从外部会话移动到 SQL Server 表是一个多步骤的过程:

+ 设计用于获取所需数据的存储过程。
+ 执行存储过程以实际获取数据。
+ 构造 INSERT 语句以指定应在何处保存检索的数据。

1. 在具有 Python 集成的系统上, 创建以下存储过程, 该存储过程使用 Python 代码来加载数据。

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    运行此代码时, 应收到消息 "命令已成功完成"。 也就是说, 该存储过程已根据您的规范创建。

2. 或者, 在具有 R 集成的系统上, 创建使用 R 的过程。

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. 若要实际填充表, 请运行存储过程, 并指定应在其中写入数据的表。 运行时, 该存储过程将执行 Python 或 R 代码, 这将加载内置的 Iris 数据集, 然后将数据插入**iris_data**表中。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果不熟悉 T-sql, 请注意 INSERT 语句仅添加新数据;它不会检查现有数据, 也不会删除和重新生成表。 若要避免在表中获取相同数据的多个副本, 可以先运行以下语句: `TRUNCATE TABLE iris_data`。 T-sql [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql)语句删除现有数据, 但保持表的结构保持不变。

    > [!TIP]
    > 若要在以后修改存储过程, 则无需删除并重新创建它。 使用[ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql)语句。 


## <a name="query-the-data"></a>查询数据

作为验证步骤, 运行查询以确认已上传数据。

1. 在对象资源管理器的 "数据库" 下, 右键单击**irissql**数据库, 然后启动一个新查询。

2. 运行一些简单的查询:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>后续步骤

在以下快速入门中, 你将创建机器学习模型, 并将其保存到表中, 然后使用该模型生成预测的结果。

+ [起步使用中的存储过程创建、定型和使用 Python 模型 SQL Server](quickstart-python-train-score-in-tsql.md)
