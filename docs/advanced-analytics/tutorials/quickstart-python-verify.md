---
title: SQL Server 中存在验证 Python 快速入门
description: 验证 SQL Server 中存在 Python 和机器学习服务的快速入门。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b0ef5d33757d9f8c4e3aed53d3867bfd5b1297b2
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513757"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>快速入门：验证 SQL Server 中是否存在 Python 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包括对数据驻留 SQL Server 数据科学分析 Python 语言支持。 脚本执行是通过存储过程，使用以下方法之一：

+ 内置[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)存储过程，传递作为输入参数中的 Python 脚本。
+ Python 脚本中的包装[自定义存储过程](sqldev-in-database-r-for-sql-developers.md)你创建的。

在此快速入门中，您将验证[SQL Server 2017 机器学习服务](../what-is-sql-server-machine-learning.md)安装和配置。

## <a name="prerequisites"></a>先决条件

本演练需要访问 SQL Server 的实例[SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)安装。

SQL Server 实例可以是 Azure 虚拟机或本地。 只需注意，外部脚本编写功能默认处于禁用状态，因此可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并确认**SQL Server Launchpad 服务**在开始之前运行。

您还需要用于运行 SQL 查询的工具。 可以运行使用任何数据库管理的 Python 脚本或查询工具，前提是它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储的过程。 本快速入门使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-python-exists"></a>验证存在 Python

你可以确认该机器学习服务 （已启用 SQL Server 实例和安装的 Python 版本。 按照以下步骤。

1. 打开 SQL Server Management Studio 并连接到 SQL Server 实例。

2. 运行下面的代码。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python`print`函数将返回到新版本**消息**窗口。 在下面的示例输出中，您可以看到 SQL Server 在这种情况下具有 Python 版本 3.5.2 安装。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

如果收到错误，有很多可以执行以确保可以进行通信的实例和 Python 的事情。

首先，排除任何安装问题。 安装后则需要配置才能启用对外部代码库的使用。 请参阅[安装 SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。 同样，请确保快速启动板服务正在运行。

您还必须添加 Windows 用户组`SQLRUserGroup`上的实例，以确保快速启动板可以提供 Python 和 SQL Server 之间的通信的登录名。 （同一个组用于这两个 R 和 Python 代码执行）。有关详细信息，请参阅[已启用隐式身份验证](../security/add-sqlrusergroup-to-database.md)。

此外，您可能需要启用已禁用的网络协议或打开防火墙，以便 SQL Server 可以与外部客户端进行通信。 有关详细信息，请参阅[安装程序疑难解答](../common-issues-external-script-execution.md)。

## <a name="call-revoscalepy-functions"></a>调用 revoscalepy 函数

若要确认**revoscalepy**不可用，运行示例脚本，以包括[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) ，所生成的统计摘要数据。 以下脚本演示如何从内置 revoscalepy 中包含的示例检索示例.xdf 数据文件。 RxOptions 函数提供**sampleDataDir**参数，它返回的示例文件的位置。

因为 rx_summary 返回类型的对象`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多个元素，可以使用 pandas 来提取只是一个表格中的数据帧。

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

## <a name="list-python-packages"></a>列出的 Python 包

Microsoft 提供大量预装了机器学习服务的 SQL Server 实例中的 Python 包。 若要查看列表中的哪些 Python 包安装，包括版本，请按照以下步骤。

1. SQL Server 实例上运行以下脚本。

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 输出是从`pip.get_installed_distributions()`在 Python 和作为返回`STDOUT`消息。

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

现在，已确认你的实例已准备好与 Python 配合使用，需要进一步了解基本的 Python 交互。

> [!div class="nextstepaction"]
> [快速入门：SQL Server 中的"hello world"Python 脚本 ](quickstart-python-run-using-t-sql.md)
