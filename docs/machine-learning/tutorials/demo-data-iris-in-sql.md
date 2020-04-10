---
title: 用于教程的 Iris 演示数据集
Description: 创建一个包含 Iris 数据集的数据库和多个预测模型。 本数据集用于 Microsoft SQL Server 机器学习服务的 R 和 Python 教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b1d3aee4034124f61d88ccdf5e35f86b13b60158
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116670"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>SQL Server 中用于 Python 和 R 教程的 Iris 演示数据 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此练习中，创建一个 SQL Server 数据库，以存储来自 [Iris 数据集](https://en.wikipedia.org/wiki/Iris_flower_data_set)的数据以及基于相同数据的模型。 Iris 数据包含在由 SQL Server 安装的 R 和 Python 发行版中，并用于 SQL Server 的机器学习教程。 

若要完成此练习，应具有 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) 或其他可以运行 T-SQL 查询的工具。

使用此数据集的教程和快速入门包括以下内容：

+  [快速入门：在 SQL Server 中创建、定型和使用带有存储过程的 Python 模型](quickstart-python-train-score-model.md)

## <a name="create-the-database"></a>创建数据库

1. 启动 SQL Server Management Studio，并打开一个新的“查询”窗口  。  

2. 为此项目创建一个新数据库，并更改“查询”窗口的上下文以使用该新数据库  。

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > 如果你不熟悉 SQL Server，或使用自己的服务器，一个常见的错误就是登录便开始操作，而没有注意到你在 master 数据库中  。 为确保使用正确的数据库，请始终使用 `USE <database name>` 语句（例如，`use irissql`）指定上下文。

3. 添加一些空表：一个用于存储数据，另一个用于存储已定型的模型。 “iris_models”表用于存储在其他练习中生成的序列化模型  。

    以下代码创建用于定型数据的表。

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
    > 如果你不熟悉 T-SQL，则需要记住 `DROP...IF` 语句。 尝试创建表并已存在表时，SQL Server 返回错误：“数据库中已存在名为‘iris_dat’的对象。” 避免这类错误的一种方法是在代码中删除任何现有的表或其他对象。

4. 运行以下代码以创建用于存储定型模型的表。 若要将 Python（或 R）模型保存在 SQL Server 中，必须将它们序列化并存储在 varbinary(max) 类型的列中  。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除模型内容之外，通常还会为其他有用的元数据添加列，例如模型的名称、定型日期、源算法和参数、源数据等等。 但现在，为简便起见，我们将只使用模型名称。

## <a name="populate-the-table"></a>填充表

可以从 R 或 Python 获取内置 Iris 数据。 可以使用 Python 或 R 将数据加载到数据帧中，然后将其插入数据库中的表中。 将定型数据从外部会话移动到 SQL Server 表中包含以下几个步骤：

+ 设计一个用于获取所需数据的存储过程。
+ 执行该存储过程以实际获取数据。
+ 构造 INSERT 语句，以指定在何处保存检索到的数据。

1. 在具有 Python 集成的系统上，创建以下使用 Python 代码加载数据的存储过程。

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

    运行此代码时，应收到消息“命令已成功完成。” 这意味着存储过程已根据你的规范创建。

2. 或者，在具有 R 集成的系统上，创建一个使用 R 的过程。

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

3. 若要实际填充表，请运行存储过程并指定应在其中写入数据的表。 运行时，存储过程执行 Python 或 R 代码，该代码加载内置 Iris 数据集，然后将数据插入“iris_data”表  。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果不熟悉 T-SQL，请注意，INSERT 语句只添加新的数据；它不会检查现有的数据，也不会删除和重新生成表。 若要避免在表中获取相同数据的多个副本，可以先运行以下语句：`TRUNCATE TABLE iris_data`。 T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) 语句可删除现有数据，但保持表结构完整。

    > [!TIP]
    > 若要在以后修改存储过程，则无需删除并重新创建。 使用 [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) 语句。 


## <a name="query-the-data"></a>查询数据

作为验证步骤，运行查询以确认已上传数据。

1. 在“对象资源管理器”中的“数据库”下，右键单击“irissql”数据库，然后启动一个新查询  。

2. 运行一些简单的查询：

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>后续步骤

在下面的快速入门中，你将创建一个机器学习模型并将其保存到表中，然后使用该模型生成预测结果。

+ [快速入门：在 SQL Server 中创建、定型和使用带有存储过程的 Python 模型](quickstart-python-train-score-model.md)
