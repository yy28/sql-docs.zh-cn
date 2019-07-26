---
title: SQL Server 中存在用于验证 Python 的快速入门
description: 用于验证 Python 和机器学习服务是否存在于 SQL Server 中的快速入门。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0dd5714f47c90c0091daacbd792b80c05ec68675
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469697"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>快速入门：验证 SQL Server 中是否存在 Python 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 包括对常驻 SQL Server 数据进行数据科学分析的 Python 语言支持。 使用以下两种方法之一通过存储过程执行脚本:

+ 内置的[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)存储过程, 将 Python 脚本作为输入参数传递。
+ 在您创建的[自定义存储过程](sqldev-in-database-r-for-sql-developers.md)中包装 Python 脚本。

在本快速入门中, 你将验证是否已安装并配置[SQL Server 2017 机器学习服务](../what-is-sql-server-machine-learning.md)。

## <a name="prerequisites"></a>系统必备

此练习需要访问安装了[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)SQL Server 的实例。

SQL Server 实例可位于 Azure 虚拟机或本地。 请注意, 默认情况下禁用外部脚本功能, 因此在开始之前, 您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

还需要一个用于运行 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行 Python 脚本, 只要它可以连接到 SQL Server 实例, 然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-python-exists"></a>验证 Python 是否存在

你可以确认机器学习服务 (为 SQL Server 实例启用了, 并安装了哪个版本的 Python。 请按照以下步骤操作。

1. 打开 SQL Server Management Studio, 然后连接到 SQL Server 实例。

2. 运行以下代码。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python `print`函数将该版本返回到 "**消息**" 窗口。 在下面的示例输出中, 可以看到在此示例中 SQL Server 安装了 Python 版本3.5.2。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

如果遇到错误, 可以执行的各种操作, 以确保实例和 Python 可以进行通信。

首先, 排除任何安装问题。 若要启用外部代码库, 必须安装安装后配置。 请参阅[安装 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。 同样, 请确保启动板服务正在运行。

还必须将 Windows 用户组`SQLRUserGroup`作为登录名添加到实例上, 以确保快速启动板可以提供 Python 和 SQL Server 之间的通信。 (相同的组用于 R 和 Python 代码执行。)有关详细信息, 请参阅[创建 SQLRUserGroup 的登录名](../security/create-a-login-for-sqlrusergroup.md)。

此外, 你可能还需要启用已禁用的网络协议, 或打开防火墙, 以便 SQL Server 能够与外部客户端进行通信。 有关详细信息, 请参阅[安装疑难解答](../common-issues-external-script-execution.md)。

## <a name="call-revoscalepy-functions"></a>调用 revoscalepy 函数

若要验证**revoscalepy**是否可用, 请运行包含生成统计摘要数据的[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)的示例脚本。 下面的脚本演示了如何从 revoscalepy 中包含的内置示例检索 xdf 数据文件。 RxOptions 函数提供了**sampleDataDir**参数, 该参数返回示例文件的位置。

由于 rx_summary 返回一个类型`class revoscalepy.functions.RxSummary.RxSummaryResults`为的对象, 该对象包含多个元素, 因此可以使用 pandas 只提取表格格式的数据帧。

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>列出 Python 包

Microsoft 提供了许多在 SQL Server 实例中预安装了机器学习服务的 Python 包。 若要查看安装了哪些 Python 包 (包括版本) 的列表, 请执行以下步骤。

1. 在 SQL Server 实例上运行以下脚本。

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 输出来自`pip.get_installed_distributions()` Python 中, 并作为`STDOUT`消息返回。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>后续步骤

现在, 你已确认你的实例可以使用 Python, 接下来请详细了解基本 Python 交互。

> [!div class="nextstepaction"]
> [起步SQL Server 中的 "Hello world" Python 脚本](quickstart-python-run-using-t-sql.md)
