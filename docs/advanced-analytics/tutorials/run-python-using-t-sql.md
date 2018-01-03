---
title: "运行 Python 使用 T-SQL |Microsoft 文档"
ms.custom: 
ms.date: 09/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: f584f98f5c30e4ca30b4f75748ee173bb2f1a257
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="run-python-using-t-sql"></a>运行 Python 使用 T-SQL

此示例演示如何运行一个简单的 Python 脚本在 SQL Server 中，通过使用存储的过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>步骤 1. 创建测试数据表

首先，你将创建一些额外的数据，则还将每周天数的名称映射到源数据时要使用。 运行下面的 T-SQL 语句，以创建表。

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>步骤 2. 运行"Hello World"脚本

下面的代码加载 Python 可执行文件、 将传递的输入的数据，并输入数据的每一行，使用一个数字，表示一天的一周索引更新表中的天名称。

记下的参数 *@RowsPerRead* 。 此参数指定 SQL Server 从传递给 Python 运行时的行的数。

Python 数据分析库，称为**pandas**，需要将数据传递到 SQL Server，并且包含默认情况下，使用机器学习服务。

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> 本快速入门中的更详细地介绍了为此存储过程参数： [T-SQL 中的使用 R 代码](rtsql-using-r-code-in-transact-sql-quickstart.md)。

## <a name="step-3-view-the-results"></a>步骤 3. 查看结果

存储的过程获取的原始数据、 将应用的 Python 脚本，然后返回中的已修改的数据**结果**Management Studio 或其他 SQL 查询工具窗格。


|DayOfWeek （之前）| Amount|DayOfWeek （之后） |
|-----|-----|-----|
|星期日|10|7|
|星期一|11.1|@shouldalert|
|星期二|12.2|2|
|星期三|13.3|3|
|星期四|14.4|4|
|星期五|15.5|5|
|星期六|16.6|6|
|星期五|17.7|5|
|星期一|18.8|@shouldalert|
|星期日|19.9|7|

状态消息或错误返回到 Python 控制台中的消息作为返回**查询**窗口。 下面是输出的你可能会看到的摘录：

*示例结果*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ **消息**输出包括用于执行脚本的工作目录。 在此示例中，MSSQLSERVER01 是指由 SQL Server 来管理该作业分配的工作帐户。 

    GUID 是执行脚本来存储数据和脚本项目期间创建的临时文件夹的名称。 这些临时文件夹保护的 SQL Server，并由 Windows 作业对象后清理脚本已终止。

+ 包含消息"Hello World"的部分会将输出两次。 这是因为值 *@RowsPerRead* 已设置为 5 和表中有 10 行; 因此，需要两次调用 Python 以处理表中的所有行。

    在生产运行过程中，我们建议使用不同的值来确定最大的应传递每个批中的行数进行试验。 最佳的行数与数据相关的而且受这两个的数据集中的列数和您传递的数据的类型。

## <a name="resources"></a>Resources

请参阅这些其他 Python 示例和高级的提示和端到端演示的教程。

+ [使用 Python revoscalepy 创建模型](use-python-revoscalepy-to-create-model.md)
+ [SQL 开发人员的数据库中 Python](sqldev-in-database-python-for-sql-developers.md)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>故障排除

如果找不到存储的过程， `sp_execute_external_script`，这意味着你可能尚未完成的配置要支持外部脚本执行的实例。 运行 SQL Server 2017 安装程序并选择后 Python 作为机器学习语言，则必须还在显式启用功能使用`sp_configure`，然后重新启动实例。 有关详细信息，请参阅[使用 Python 的安装程序机器学习服务](../python/setup-python-machine-learning-services.md)。