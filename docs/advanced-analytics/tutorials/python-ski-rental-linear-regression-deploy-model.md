---
title: Python 教程：部署模型
description: 本教程系列由四个部分组成，在第四部分中，你将使用机器学习服务将 Python 模型部署到 SQL Server 数据库中，以预测雪橇租赁次数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e78f099f108f9affa58f53d1ad46b802eae004dd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75681719"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-to-sql-server-machine-learning-services"></a>Python 教程：将线性回归模型部署到 SQL Server 机器学习服务中
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本教程系列由四个部分组成，在第四部分中，你将使用机器学习服务将在 Python 中开发的线性回归模型部署到 SQL Server 数据库中。

本文将指导如何进行以下操作：

> [!div class="checklist"]
> * 创建生成机器学习模型的存储过程
> * 将模型存储在数据库表中
> * 创建使用模型进行预测的存储过程
> * 使用新数据执行模型

在[第一部分](python-ski-rental-linear-regression.md)中，你了解了如何还原示例数据库。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，你了解了如何将数据从 SQL Server 加载到 Python 数据框架，并在 Python 中准备数据。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，你了解了如何在 Python 中定型线性回归机器学习模型。

## <a name="prerequisites"></a>先决条件

* 本教程的第四部分假设你已完成了[第一部分](python-ski-rental-linear-regression.md)和其中的必备条件。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>创建生成模型的存储过程

现在，通过使用开发的 Python 脚本来创建存储过程 generate_rental_py_model  ，此存储过程会使用 scikit-learn 中的 LinearRegression 来定型和生成线性回归模型。

在 Azure Data Studio 中运行以下 T-SQL 语句，从而创建存储过程来定型模型。

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>将模型存储在数据库表中

在 TutorialDB 数据库中创建一个表，然后将模型保存到表中。

1. 在 Azure Data Studio 中运行以下 T-SQL 语句来创建名为 dbo.rental_py_models 的表，用于存储模型  。

   ```sql
   USE TutorialDB;
   DROP TABLE IF EXISTS dbo.rental_py_models;
   GO
   CREATE TABLE dbo.rental_py_models (
       model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
       model VARBINARY(MAX) NOT NULL
   );
   GO
   ```

1. 将模型作为二进制对象保存到表中，模型名为 linear_model  。

   ```sql
   DECLARE @model VARBINARY(MAX);
   EXECUTE generate_rental_py_model @model OUTPUT;
   
   INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
   ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>创建进行预测的存储过程

1. 创建存储过程 py_predict_rentalcount，此过程会使用已定型的模型和一组新数据来进行预测  。 在 Azure Data Studio 中运行以下 T-SQL。

   ```sql
   DROP PROCEDURE IF EXISTS py_predict_rentalcount;
   GO
   CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
   AS
   BEGIN
    DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
   
    EXECUTE sp_execute_external_script
                @language = N'Python',
                @script = N'
   
   # Import the scikit-learn function to compute error.
   from sklearn.metrics import mean_squared_error
   import pickle
   import pandas
   
   rental_model = pickle.loads(py_model)
   
   df = rental_score_data
   
   # Get all the columns from the dataframe.
   columns = df.columns.tolist()
   
   # Variable you will be predicting on.
   target = "RentalCount"
   
   # Generate the predictions for the test set.
   lin_predictions = rental_model.predict(df[columns])
   print(lin_predictions)
   
   # Compute error between the test predictions and the actual values.
   lin_mse = mean_squared_error(lin_predictions, df[target])
   #print(lin_mse)
   
   predictions_df = pandas.DataFrame(lin_predictions)
   
   OutputDataSet = pandas.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
   '
   , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
   , @input_data_1_name = N'rental_score_data'
   , @params = N'@py_model varbinary(max)'
   , @py_model = @py_model
   with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
   
   END;
   GO
    ```

1. 创建用于存储预测的表。

   ```sql
   DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
   GO
   
   CREATE TABLE [dbo].[py_rental_predictions](
    [RentalCount_Predicted] [int] NULL,
    [RentalCount_Actual] [int] NULL,
    [Month] [int] NULL,
    [Day] [int] NULL,
    [WeekDay] [int] NULL,
    [Snow] [int] NULL,
    [Holiday] [int] NULL,
    [Year] [int] NULL
   ) ON [PRIMARY]
   GO
   ```

1. 执行此存储过程来预测租赁计数

   ```sql
   --Insert the results of the predictions for test set into a table
   INSERT INTO py_rental_predictions
   EXEC py_predict_rentalcount 'linear_model';
   
   -- Select contents of the table
   SELECT * FROM py_rental_predictions;
   ```

   可得到类似于下面的结果。

   :::image type="content" source="media/python-tutorial-prediction-results.png" alt-text="来自存储过程的预测结果":::

你已经成功地在 SQL Server 机器学习服务中创建、定型和部署了模型。 然后，你在存储过程中使用了该模型来基于新数据对值进行预测。

## <a name="next-steps"></a>后续步骤

在本教程系列的第四部分中，你完成了这些步骤：

* 创建生成机器学习模型的存储过程
* 将模型存储在数据库表中
* 创建使用模型进行预测的存储过程
* 使用新数据执行模型

若要了解关于在 SQL Server 机器学习服务中使用 Python 的详细信息，请参阅：

+ [SQL Server 机器学习服务的 Python 教程](sql-server-python-tutorials.md)
