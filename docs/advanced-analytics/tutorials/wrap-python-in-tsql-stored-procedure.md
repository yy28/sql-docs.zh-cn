---
title: 将 Python 代码包装在存储过程 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b0c32ba91698345adea542ed5929a494b00059e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>将 Python 代码包装在存储过程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在[上一课](run-python-using-t-sql.md)，您学习了如何将 Python 与 SQL Server 通信。 在本课程中，你将学习如何将 Python 代码嵌入在存储过程，以从 Python 示例数据集，获取数据并将该数据写入到的 SQL Server 表。

系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)提供包装器将 SQL 变量和 SQL 数据集传递到 Python。 它还处理 Python 输出的结果，并将其传递给 SQL Server 的格式与 SQL 数据类型兼容。

我们来看这如何工作。

## <a name="prepare-the-database-and-tables"></a>准备的数据库和表

但也可以设置远程客户端和运行 Python 代码使用 Visual Studio Code、 Visual Studio、 PyCharm，或其他工具，来简化此方案中，应作为存储过程的一部分运行在本课程中的所有代码。

1. 启动 SQL Server Management Studio，并打开一个新**查询**窗口。  

2. 创建新数据库对于此项目，并更改的上下文你**查询**窗口以便使用新的数据库。

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > 如果你熟悉 SQL Server，或您自己的服务器上工作，一个常见错误是登录并开始而无需注意到你正在使用**master**数据库。 若要确保你正在使用正确的数据库，始终指定上下文使用`USE <database name>`语句。

3. 添加一些空表： 一个以用于存储数据，和一个以用于存储你训练的模型。 稍后你填充使用 Python 的表。

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

    如果你不熟悉 T-SQL 的它支付需记住`DROP...IF`语句。 如果你尝试创建一个表并且已经存在一个，SQL Server 将返回错误:"已存在名为 iris_data 数据库中的对象。" 若要避免此类错误的一种方法是代码的作为你的一部分删除任何现有表或其他对象。

4. 运行下面的代码以创建用于存储经过训练的模型的表。 若要在 SQL Server 中保存 Python （或 R） 的模型，它们必须序列化和存储的类型列中**varbinary （max)**。 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    除了模型内容中，通常情况下，你将添加其他有用的元数据，例如模型的名称、 它进行定型的日期源算法和参数，源数据的列和等等。 我们现在使其保持简单，请仅使用模型名称。

## <a name="populate-the-table"></a>填充表

若要将定型数据从 Python 移到 SQL Server 表是一个多步骤过程：

+ 设计获取所需的数据的存储的过程。
+ 执行存储的过程以实际获取数据。
+ 使用 INSERT 语句指定检索到的数据应保存位置。

1. 创建以下存储的过程，其中包含的 Python 代码。 

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

    当你运行此代码时，你应收到消息"命令已成功完成。" 这意味着是存储的过程已创建根据您的规范。

2. 若要实际填充表，运行存储的过程，并指定应在其中写入数据的表。 当运行时，存储的过程执行 Python 代码，此操作将 Iris 数据集加载从内置的 Python 示例数据。

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    如果你不熟悉 T-SQL 的请注意 INSERT 语句仅添加新数据;它不会检查有现有的数据，或删除并重新生成表。 若要避免在表中获取的相同的数据的多个副本，可以运行此语句，首先： `TRUNCATE TABLE iris_data`。 T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql)语句删除现有的数据，同时还表的结构保持不变。

    > [!TIP]
    > 若要将存储的过程修改为更高版本，不需要删除并重新创建它。 使用[ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql)语句。 

3. 若要验证正确加载了数据，可以运行一些简单的查询：

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

在[下一课中](../tutorials/train-score-using-python-in-tsql.md)，创建机器学习模型，并将其保存到表。

### <a name="further-reading-about-stored-procedures"></a>有关存储过程的其他阅读材料

如果你不熟悉 SQL Server，你可能会发现在第一个复杂的存储的过程。 但是，存储的过程是一个功能强大且灵活的接口，用于在应用程序和服务器之间传递数据。 通过使用存储的过程，你可以动态定义输入，这样就容易相互传递中新的模型名称、 新的参数，并将新数据，而无需更改你的 Python 代码。

存储过程工作原理的概述，请参阅[存储过程 （数据库引擎）](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine)，或本教程：[编写 TRANSACT-SQL 语句](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)。

也有一些良好教程在社区站点如[SQL Server 中央](http://www.sqlservercentral.com/)或[SQL 团队](http://www.sqlteam.com/)。

在你考虑如何最封装在 T-SQL 中的 Python 代码，还请考虑使用这些功能：

+ 定义存储过程的默认值
+ 使用 OUTPUT 关键字来通过输入变量传递
+ 创建使用与结果以确保应用程序使用该数据的架构定义具有正确的数据类型和列名称
+ 给出提示，以提高批处理
+ 模拟不同的用户来测试你的代码，使用 EXECUTE AS 子句

## <a name="next-lesson"></a>下一课

[训练 Python 模型和 SQL Server 中生成评分](../tutorials/train-score-using-python-in-tsql.md)