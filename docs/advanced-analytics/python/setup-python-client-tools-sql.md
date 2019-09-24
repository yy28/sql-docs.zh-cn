---
title: 为 Python 开发设置数据科学客户端
description: 设置 Python 本地环境 (Jupyter Notebook 或 PyCharm) 以便远程连接到使用 Python SQL Server 的机器学习服务。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 87c05fafb122e292c45033bb019548c84df44de0
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199476"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>在 SQL Server 上设置用于 Python 开发的数据科学客户端机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

如果在[机器学习服务 (数据库内) 安装](../install/sql-machine-learning-services-windows-install.md)中包括 python 选项, 则从 SQL Server 2017 或更高版本开始提供 python 集成。 

若要为 SQL Server 开发和部署 Python 解决方案, 请在开发工作站上安装 Microsoft 的[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和其他 Python 库。 Revoscalepy 库也位于远程 SQL Server 实例上, 协调两个系统之间的计算请求。 

本文介绍如何配置 Python 开发工作站, 以便能够与启用机器学习和 Python 集成的远程 SQL Server 进行交互。 完成本文中的步骤后, 你将拥有与 SQL Server 上的相同的 Python 库。 你还将了解如何将计算从本地 Python 会话推送到 SQL Server 上的远程 Python 会话。

![客户端-服务器组件](media/sqlmls-python-client-revo.png "本地和远程 Python 会话和库")

若要验证安装, 你可以使用本文中所述的内置 Jupyter 笔记本, 或将[库链接](#install-ide)到你通常使用的 PyCharm 或其他任何 IDE。

> [!Tip]
> 有关这些练习的视频演示, 请参阅[从 Jupyter 笔记本的 SQL Server 远程运行 R 和 Python](https://youtu.be/D5erljpJDjE)。

> [!Note]
> 客户端库安装的替代方法是使用[独立服务器](../install/sql-machine-learning-standalone-windows-install.md)作为富客户端，一些客户更喜欢使用它来完成更深入的方案工作。 独立服务器与 SQL Server 完全分离, 但由于它具有相同的 Python 库, 因此可以将它用作 SQL Server 数据库内分析的客户端。 还可以将其用于与SQL无关的工作，包括从其他数据平台导入数据和对数据建模。 如果安装独立服务器, 可以在以下位置找到 Python 可执行文件: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 若要验证安装, 请在该位置使用 Python[打开 Jupyter 笔记本](#python-tools)以运行命令。

## <a name="commonly-used-tools"></a>常用工具

无论你是 SQL 的 Python 开发人员还是新的针对 Python 和数据库内分析的 SQL 开发人员, 都需要一个 Python 开发工具和一个 T-sql 查询编辑器 (如[SQL Server Management Studio (SSMS))](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)来执行数据库内分析。

对于 Python 开发, 你可以使用 Jupyter 笔记本, 它随附在 SQL Server 安装的 Anaconda 分发中。 本文介绍如何启动 Jupyter 笔记本, 以便可以在 SQL Server 本地和远程运行 Python 代码。

SSMS 是一个单独的下载, 适用于在 SQL Server 上创建和运行存储过程, 包括包含 Python 代码的存储过程。 几乎在 Jupyter 笔记本中编写的任何 Python 代码都可以嵌入到存储过程中。 可以逐步执行其他快速入门, 了解[SSMS 和 Embedded Python](../tutorials/quickstart-python-create-script.md)。

## <a name="1---install-python-packages"></a>1-安装 Python 包

本地工作站必须具有与 SQL Server 上的 Python 包版本相同的 Python 包版本, 包括使用 Python 3.5.2 分发的基本 Anaconda 4.2.0 和 Microsoft 特定的包。

安装脚本将三个 Microsoft 特定的库添加到 Python 客户端。 该脚本将安装[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), 用于定义数据源对象和计算上下文。 它安装提供机器学习算法的[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 。 还安装了[azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)包, 但它适用于与独立 (非实例) Machine Learning Server 上下文相关联的操作化任务, 并且可能对数据库内分析的使用有限。

1. 下载安装脚本。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)安装 Microsoft Python 包的版本9.2.1。 此版本对应于默认 SQL Server 实例。 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)安装 Microsoft Python 包版本9.3。 如果远程 SQL Server 实例[绑定到 Machine Learning Server 9.3](../install/upgrade-r-and-python.md)，则此版本是更好的选择。

2. 使用提升的管理员权限打开 PowerShell 窗口 (右键单击 "以**管理员身份运行**")。

3. 中转到下载安装程序的文件夹, 然后运行该脚本。 `-InstallFolder`添加命令行参数以指定库的文件夹位置。 例如： 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

如果省略安装文件夹, 则默认值为 C:\Program Files\Microsoft\PyForMLS。

安装需要一些时间才能完成。 可在 PowerShell 窗口中监视进度。 安装完成后, 你将获得一组完整的程序包。 

> [!Tip] 
> 对于在 Windows 上运行 Python 程序的一般 purppose 信息, 我们建议采用[适用于 windows 的 PYTHON 常见问题解答](https://docs.python.org/3/faq/windows.html)。

## <a name="2---locate-executables"></a>2-查找可执行文件

仍在 PowerShell 中列出安装文件夹的内容, 以确认已安装了 Python、脚本和其他包。 

1. 输入`cd \`以进入根驱动器, 然后输入在上一步中为指定的`-InstallFolder`路径。 如果在安装过程中省略此参数, 则默认`cd C:\Program Files\Microsoft\PyForMLS`值为。

2. 输入`dir *.exe`以列出可执行文件。 应会看到 " **python**"、" **pythonw**" 和 " **uninstall-anaconda**"。

  ![Python 可执行文件列表](media/powershell-python-exe.png)
   
在具有多个版本的 Python 的系统上, 如果要加载**revoscalepy**和其他 Microsoft 包, 请记住使用此特定 Python。

> [!Note] 
> 安装脚本不会修改计算机上的 PATH 环境变量, 这意味着你刚安装的新 python 解释器和模块不会自动提供给你可能具有的其他工具。 有关将 Python 解释器和库链接到工具的帮助, 请参阅[安装 IDE](#install-ide)。

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-打开 Jupyter 笔记本

Anaconda 包括 Jupyter 笔记本。 下一步是创建笔记本, 并运行包含刚才安装的库的某些 Python 代码。

1. 在 Powershell 提示符下, 在 C:\Program Files\Microsoft\PyForMLS 目录中, 打开 "脚本" 文件夹中的 Jupyter 笔记本:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  笔记本应在默认浏览器`https://localhost:8889/tree`中打开。

  另一种方法是双击 " **jupyter-notebook**"。 

2. 单击 "**新建**", 然后单击 " **Python 3**"。

  ![新 Python 3 选择的 jupyter 笔记本](media/jupyter-notebook-new-p3.png)

3. 输入`import revoscalepy`并运行命令, 加载一个特定于 Microsoft 的库。

4. 输入并运行`print(revoscalepy.__version__)`以返回版本信息。 应会看到 "9.2.1" 或 "9.3.0"。 可以[在服务器上的 revoscalepy 中](../package-management/r-package-information.md)使用这两个版本中的任何一个。

4. 输入一系列更复杂的语句。 此示例使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)通过本地数据集生成汇总统计信息。 其他函数获取示例数据的位置, 并为 xdf 文件创建数据源对象。

  ```python
  import os
  from revoscalepy import rx_summary
  from revoscalepy import RxXdfData
  from revoscalepy import RxOptions
  sample_data_path = RxOptions.get_option("sampleDataDir")
  print(sample_data_path)
  ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
  summary = rx_summary("ArrDelay+DayOfWeek", ds)
  print(summary)
  ```

下面的屏幕截图显示了输入和输出部分, 为简洁起见进行了修整。

  ![显示 revoscalepy 输入和输出的 jupyter 笔记本](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-获取 SQL 权限

若要连接到 SQL Server 实例以运行脚本和上传数据, 必须在数据库服务器上具有有效登录。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议你使用 Windows 集成身份验证, 但对于某些方案, 使用 SQL 登录更简单, 特别是当你的脚本包含外部数据的连接字符串时。

用于运行代码的帐户至少必须具有读取正在处理的数据库的权限, 以及执行任何外部脚本的特殊权限。 大多数开发人员还需要创建存储过程的权限, 并将数据写入包含定型数据或评分数据的表中。 

要求数据库管理员在使用 Python 的数据库中[为你的帐户配置以下权限](../security/user-permission.md):

+ **执行任何外部脚本**以在服务器上运行 Python。
+ 用于运行用于定型模型的查询的**db_datareader**权限。
+ 用于编写定型数据或评分数据的**db_datawriter** 。
+ **db_owner**来创建存储过程、表和函数等对象。 
  还需要**db_owner**来创建示例数据库和测试数据库。 

如果你的代码需要 SQL Server 默认情况下未安装的包, 请与数据库管理员一起将包与实例一起安装。 SQL Server 是一种受保护的环境, 对包的安装位置有一些限制。 即使您有权限, 也不建议将程序包即席安装为您的代码的一部分。 此外, 在服务器库中安装新包之前, 请务必仔细考虑安全问题。


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-创建测试数据

如果您有权在远程服务器上创建数据库, 则可以运行以下代码来创建用于本文剩余步骤的 Iris 演示数据库。

### <a name="1---create-the-irissql-database-remotely"></a>1-远程创建 irissql 数据库

```python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2-从 Spark-sklearn 导入 Iris 示例

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 Revoscalepy Api 创建表并加载 Iris 数据

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-测试远程连接

在尝试下一步之前, 请确保对 SQL Server 实例和[Iris 示例数据库](../tutorials/demo-data-iris-in-sql.md)的连接字符串具有权限。 如果数据库不存在, 并且您有足够的权限, 则可以[使用这些内联说明创建数据库](#create-iris-remotely)。

将连接字符串替换为有效的值。 示例代码使用`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` , 但你的代码应指定远程服务器 (可能使用实例名称) 以及映射到数据库用户登录名的凭据选项。

### <a name="define-a-function"></a>定义函数

下面的代码定义一个函数, 该函数将发送到后面的步骤中 SQL Server。 执行时, 它使用远程服务器上的数据和库 (revoscalepy、pandas、matplotlib) 创建 iris 数据集的散点图。 它将 png 的 bytestream 返回到 Jupyter 笔记本, 以在浏览器中呈现。

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>将函数发送到 SQL Server

在此示例中，创建远程计算上下文，然后将该函数的执行发送到与[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)SQL Server。 **Rx_exec**函数很有用，因为它将计算上下文作为参数接受。 要远程执行的任何函数都必须具有计算上下文参数。 某些函数（如[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) ）将直接支持此参数。 对于不执行的操作，你可以使用**rx_exec**在远程计算上下文中传递你的代码。

在此示例中, 不需要将原始数据从 SQL Server 传输到 Jupyter Notebook 中。 所有计算都发生在 Iris 数据库中, 并且仅将映像文件返回给客户端。

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

以下屏幕截图显示了输入和散点图输出。

  ![显示散点图输出的 jupyter 笔记本](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-从工具启动 Python

由于开发人员经常使用多个版本的 Python, 因此安装程序不会将 Python 添加到你的路径。 若要使用安装程序安装的 Python 可执行文件和库, 请将你的 IDE 链接到也提供了**revoscalepy**和**microsoftml**的路径上的**Python。** 

### <a name="command-line"></a>命令行

如果从 C:\Program Files\Microsoft\PyForMLS (或你为 Python 客户端库安装指定的任何位置) 运行**Python** , 则可以访问完整的 Anaconda 分发以及 Microsoft python 模块**revoscalepy**和**microsoftml**。

1. 请参阅 C:\Program Files\Microsoft\PyForMLS, 然后双击 " **Python**"。
2. 开放式交互式帮助:`help()`
3. 在帮助提示符下键入模块的名称: `help> revoscalepy`。 "帮助" 返回 "名称"、"包内容"、"版本" 和 "文件位置"。
4. 在**help >** 提示符下返回版本和包信息: `revoscalepy`。 按 Enter 几次, 退出帮助。
5. 导入模块:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter 笔记本

本文使用内置 Jupyter 笔记本演示对**revoscalepy**的函数调用。 如果你不熟悉此工具, 下面的屏幕截图说明了这些部分如何组合在一起, 并说明了它们为什么全部 "工作"。 

父文件夹 C:\Program Files\Microsoft\PyForMLS 包含 Anaconda 和 Microsoft 程序包。 Jupyter 笔记本包含在 Anaconda 中的 "脚本" 文件夹下, Python 可执行文件是通过 Jupyter 笔记本自动注册的。 在站点包下找到的包可以导入到笔记本, 其中包括用于数据科学和机器学习的三个 Microsoft 包。

  ![可执行文件和库](media/jupyter-notebook-python-registration.png)

如果使用其他 IDE, 则需要将 Python 可执行文件和函数库链接到工具。 以下部分提供了常用工具的说明。

### <a name="visual-studio"></a>Visual Studio

如果已[在 Visual Studio 中使用 python](https://code.visualstudio.com/docs/languages/python), 请使用以下配置选项创建包含 Microsoft python 包的 python 环境。

| 配置设置 | value |
|-----------------------|-------|
| **前缀路径** | C:\Program Files\Microsoft\PyForMLS |
| **解释器路径** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **窗口化解释器** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

有关配置 Python 环境的帮助, 请参阅[在 Visual Studio 中管理 Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

### <a name="pycharm"></a>PyCharm

在 PyCharm 中, 将解释器设置为 Machine Learning Server 安装的 Python 可执行文件。

1. 在新项目中, 在 "设置" 中单击 "**添加本地**"。

2. 输入`C:\Program Files\Microsoft\PyForMLS\`。

你现在可以导入**revoscalepy**、 **microsoftml**或**azureml**模块。 还可以选择 "**工具** > " "**Python 控制台**" 打开交互窗口。

## <a name="next-steps"></a>后续步骤

现在, 你已有工具和 SQL Server 的工作连接, 请通过使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)通过 Python 快速入门来扩展你的技能。

> [!div class="nextstepaction"]
> [快速入门：利用 SQL Server 机器学习服务创建和运行简单的 Python 脚本](../tutorials/quickstart-python-create-script.md)