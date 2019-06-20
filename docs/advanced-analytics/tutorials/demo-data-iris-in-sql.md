---
title: 用于 Python 和 R 教程-SQL Server 机器学习的鸢尾花演示数据集
Description: 创建一个包含鸢尾花数据集和表以存储模型数据库。 在练习显示如何在 SQL Server 存储过程中包装 R 语言或 Python 代码中使用此数据集。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f4a57f89a89ed8d5cbf81cc3d63fc1f19b42e51a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641067"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>鸢尾花演示数据的 SQL Server 中的 Python 和 R 教程 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此练习中，创建一个 SQL Server 数据库来存储中的数据[鸢尾花卉数据集](https://en.wikipedia.org/wiki/Iris_flower_data_set)和基于相同的数据模型。 鸢尾花数据包含在 SQL Server 安装的 R 和 Python 分发版和用于 SQL Server 中机器学习教程。 

若要完成此练习中，您应有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或另一个工具，可运行 T-SQL 查询。

教程和快速入门使用此数据集包括：

+  [快速入门：创建、 定型和 SQL Server 中使用存储过程中使用 Python 模型](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>创建数据库

1. 启动 SQL Server Management Studio，并打开一个新**查询**窗口。  

2. 创建新的数据库对于此项目，并将更改的上下文你**查询**窗口以便使用新的数据库。

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > 如果你是刚接触 SQL Server，或者你拥有的服务器上工作，一个常见错误是以用户身份登录并启动工作不会引起你正在**主**数据库。 若要确保使用正确的数据库，始终指定上下文中使用`USE <database name>`语句 (例如， `use irissql`)。

3. 添加一些空表： 一个用于存储的数据，另一个用于存储的训练的模型。 **Iris_models**表用于存储在其他练习中生成的序列化的模型。

    下面的代码创建用于定型数据的表。

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
    > 如果您不熟悉 T-SQL，应该先记住`DROP...IF`语句。 当你尝试创建一个表并已存在时，SQL Server 将返回错误："没有已名为 iris_data' 在数据库中的对象。" 若要避免此类错误的一种方法是代码的作为你的一部分删除任何现有表或其他对象。

4. 运行以下代码以创建用于存储已训练的模型的表。 若要保存在 SQL Server 中的 Python （或 R） 模型，它们必须序列化和存储的列中的类型**varbinary （max)**。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除了模型内容中，通常情况下，你将还添加其他有用的元数据，例如模型的名称、 日期进行训练，源算法和参数，源数据列等。 现在我们将简单地说，并使用只是模型名称。

## <a name="populate-the-table"></a>填充表

可以从 R 或 Python 获取内置鸢尾花数据。 可以使用 Python 或 R 将数据加载到数据帧，然后将其插入到数据库中的表。 将训练数据从外部的会话移动到 SQL Server 表是一个多步骤过程：

+ 设计存储的过程，可获取所需的数据。
+ 执行存储的过程来实际获取数据。
+ 构造一个 INSERT 语句以指定应在其中保存检索到的数据。

1. 在系统上使用 Python 集成，创建以下使用 Python 代码来加载数据的存储的过程。

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

    当运行此代码时，你应收到消息"命令已成功完成。" 这意味着是存储的过程已创建根据您的规范。

2. 或者，在具有 R 集成的系统，创建改为使用 R 的过程。

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

3. 若要实际填充表，运行存储的过程并指定应在其中写入数据的表。 当运行时，存储的过程执行 Python 或 R 代码，也不能加载内置的鸢尾花数据集，然后将数据插入**iris_data**表。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果您熟悉 T-SQL，请注意 INSERT 语句仅添加新数据;它不会检查有现有的数据，或删除并重新生成表。 若要避免在表中获取相同的数据的多个副本，可以首先运行此语句： `TRUNCATE TABLE iris_data`。 T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql)语句删除现有数据，但保留表的结构保持不变。

    > [!TIP]
    > 若要修改存储的过程更高版本，不需要删除并重新创建它。 使用[ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql)语句。 


## <a name="query-the-data"></a>查询数据

作为验证步骤，运行查询以确认数据已上传。

1. 在对象资源管理器，在数据库中右键单击**irissql**数据库，然后启动一个新查询。

2. 运行一些简单的查询：

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>后续步骤

在以下快速入门中，将创建机器学习模型并将其保存到表中，然后使用该模型生成预测的结果。

+ [快速入门：创建、 定型和 SQL Server 中使用存储过程中使用 Python 模型](quickstart-python-train-score-in-tsql.md)
