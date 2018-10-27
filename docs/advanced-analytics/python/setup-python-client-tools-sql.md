---
title: 设置为用于 SQL Server 机器学习 Python 客户端 |Microsoft Docs
description: 设置远程连接到 SQL Server 机器学习服务与 Python 配合使用的 Python 本地环境。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 326676d1be684b90784351de316590ebdb1ff29f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051149"
---
# <a name="set-up-a-python-client-for-use-with-sql-server-machine-learning"></a>设置为用于 SQL Server 机器学习 Python 客户端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

从机器学习服务 （数据库） 安装中包括的 Python 选项时开始在 SQL Server 2017 或更高版本提供 Python 集成。 有关详细信息，请参阅[安装 SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。

在本文中，了解如何配置客户端开发工作站，以便可以连接到远程 SQL Server 启用了机器学习和 Python 集成。 在结束时，必须将相同的 Python 库作为 SQL 服务器上并可以将计算推送从与 SQL Server 上的远程会话的本地会话。

> [!Tip]
> 有关视频演示，请参阅[运行 R 和远程 SQL Server 从 Jupyter 笔记本中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)。

> [!Note]
> 安装只需客户端库的替代方法使用独立的服务器。 使用独立的丰富的客户端与服务器是某些客户更喜欢更多的端到端方案中工作的一个选项。 如果有[独立服务器](../install/sql-machine-learning-standalone-windows-install.md)提供在 SQL Server 安装程序，必须从 SQL Server 数据库引擎实例完全分离的 Python 服务器。 Standalon server 包括开放源代码基础发行版的 Anaconda 以及特定于 Microsoft 的库。 您可以找到在此位置的 Python 可执行文件： `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 验证富客户端安装时，以打开[Jupyter 笔记本](#python-tools)以使用 Python.exe 在服务器上运行命令。

## <a name="1---install-python-packages"></a>1-安装 Python 包

本地工作站必须具有相同的 Python 包版本的 SQL Server，包括基础发行版和特定于 Microsoft 的包上[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)并[microsftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 [Azureml 模型管理](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)还安装包，但也适用于与独立 （非实例） 的机器学习服务器上下文关联的操作化任务。 对于 SQL Server 实例上的数据库内分析，操作化是通过存储过程。

1. 下载安装脚本，以便使用 Python 3.5.2 安装 Anaconda 4.2.0 和三个以前列出的 Microsoft 包。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) 如果不是 SQL Server 2017 绑定 （常见情况）。 如果你不确定，请选择此脚本。

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 如果远程 SQL Server 实例是[绑定到机器学习服务器 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

2. 使用提升的管理员权限打开 PowerShell 窗口 (右键单击**以管理员身份运行**)。

3. 转到下载安装程序的文件夹并运行该脚本。 添加`-InstallFolder`命令行参数来指定库的文件夹位置。 例如： 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

如果省略安装文件夹，默认值为 C:\Program Files\Microsoft\PyForMLS。

安装需要一些时间才能完成。 你可以监视在 PowerShell 窗口中的进度。 安装程序完成后，你有一组完整的包。 

> [!Tip] 
> 我们建议[Python 为 Windows 常见问题](https://docs.python.org/3/faq/windows.html)有关在 Windows 上运行 Python 程序的常规 purppose 信息。

## <a name="2---locate-executables"></a>2-查找可执行文件

仍在 PowerShell 中，导航到安装文件夹，以确认 Python.exe、 脚本和其他包的位置。 

1. 输入`cd \`以转到根驱动器，然后输入为指定的路径`-InstallFolder`在上一步。 如果在安装过程中省略此参数，默认值是`cd C:\Program Files\Microsoft\PyForMLS`。

2. 输入`dir *.exe`若要列出可执行文件。 应会看到**python.exe**， **pythonw.exe**，并**卸载 anaconda.exe**。

  ![Python 可执行文件的列表](media/powershell-python-exe.png)
   
在系统上将多个版本的 Python，请记住如果您想要加载，请使用此特定 Python.exe **revoscalepy**和其他 Microsoft 包。

> [!Note] 
> 安装脚本不会修改你在计算机上，这意味着新的 python 解释器和您刚刚安装的模块不自动提供给可能有其他工具的 PATH 环境变量。 将 Python 解释器和库链接到工具的帮助，请参阅[安装 IDE](#install-ide)。

<a name="python-tool"></a>

## <a name="3---open-jupyter-notebooks"></a>3-打开 Jupyter Notebook

Anaconda 包含的 Jupyter 笔记本。 下一步，创建一个 notebook 并运行包含您刚安装的库的某些 Python 代码。

1. 在 Powershell 提示符处，导航到脚本文件夹打开 Jupyter Notebook:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

  应该在默认浏览器中打开笔记本`http://localhost:8889/tree`。

2. 单击**新建**，然后单击**Python 3**。

  ![使用新的 Python 3 选择的 jupyter 笔记本](media/jupyter-notebook-new-p3.png)

3. 输入`import revoscalepy`并运行到加载特定于 Microsoft 的库的命令。

4. 输入一系列更复杂的语句。 此示例生成汇总统计信息使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)对本地数据集。 其他函数获取示例数据的位置，并创建本地.xdf 文件的数据源对象。

  ```Python
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

以下屏幕截图显示的输入和输出中，已简化的一部分。

  ![显示 revoscalepy 输入和输出的 jupyter 笔记本](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-获取 SQL 权限

若要连接到要运行脚本和上传数据的 SQL Server 实例，必须在数据库服务器上具有有效的登录名。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议使用 Windows 集成身份验证，但使用 SQL 登录名是在某些情况下，更简单，尤其是在脚本中包含对外部数据连接字符串时。

最小值，用来运行代码的帐户必须具有你正在使用，加上特殊权限执行任意外部脚本从数据库中读取的权限。 大多数开发人员还需要权限才能创建存储的过程，并将数据写入到包含训练数据的表或评分的数据。 

询问数据库管理员可以在其中使用 Python 在数据库中配置的帐户的以下权限：

+ **EXECUTE ANY EXTERNAL SCRIPT**若要在服务器上运行 Python。
+ **db_datareader**权限才能运行用于定型模型的查询。
+ **db_datawriter**编写定型数据或评分的数据。
+ **db_owner**以创建对象的存储过程，如表、 函数。 
  您还需要**db_owner**创建示例，并测试数据库。 

如果你的代码需要与 SQL Server 的默认情况下不安装的程序包，排列与数据库管理员能够与实例安装的包。 SQL Server 是一个受保护的环境并在其中安装包的限制。 不建议临时安装的包作为你的代码的一部分，即使您具有权限。 此外，server 库中安装新包之前始终仔细考虑的安全隐患。

## <a name="5---test-remote-connection"></a>5-测试远程连接

此下一步之前，请确保您具有 SQL Server 实例和连接字符串上的权限[鸢尾花示例数据库](../tutorials/demo-data-iris-in-sql.md)。 如果数据库不存在并且具有足够的权限，则可以[使用这些内联说明创建数据库](#create-iris-remotely)。

连接字符串替换为有效的值。 示例代码使用`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`，但你的代码应具有实例名称可能是指定的远程服务器。

### <a name="define-a-function"></a>定义一个函数

以下代码定义一个函数，将在后面的步骤发送到 SQL Server。 执行时，它使用数据和库 （revoscalepy，pandas，matplotlib） 在远程服务器上创建散点图的鸢尾花数据集。 它将返回.png 字节的流返回到要呈现在浏览器中的 Jupyter 笔记本。

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

### <a name="send-the-function-to-sql-server"></a>将该函数发送到 SQL Server

在此示例中，创建远程计算上下文，然后将函数的执行发送到 SQL Server [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)。 **Rx_exec**函数很有用，因为它接受作为参数的计算上下文。 你想要远程执行的任何函数必须具有的计算上下文参数。 一些函数，如[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)直接支持此参数。 对于不的操作，可以使用**rx_exec**在远程计算上下文中提供你的代码。

在此示例中，没有原始数据必须从 SQL Server 传输到 Jupyter Notebook。 鸢尾花数据库中发生的所有计算，只有图像文件返回到客户端。

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

下面的屏幕截图显示了输入和散点图输出。

  ![jupyter 笔记本显示散点图输出](media/jupyter-notebook-scatterplot.png)

## <a name="6---link-ide-to-pythonexe"></a>6-链接到 python.exe 的 IDE

如果只要调试脚本从命令行，您可以通过获取的标准的 Python 工具。 但是，如果你正在开发新的解决方案，您可能需要为完备的 Python IDE。 常用选项包括：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)与 Python 配合使用
+ [用于 Visual Studio 的 AI 工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [在 Visual Studio Code 中的 Python](https://code.visualstudio.com/docs/languages/python)
+ 常用的第三方工具如 PyCharm、 Spyder 和 Eclipse

我们建议 Visual Studio，因为它支持数据库项目，以及机器学习项目。 为了帮助您配置的 Python 环境，请参阅[Visual Studio 中的管理 Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

因为开发人员经常使用多个版本的 Python，安装程序不向路径添加 Python。 若要使用的 Python 可执行文件和由安装程序安装的库，链接到你的 IDE **Python.exe**还提供的路径处**revoscalepy**并**microsoftml**。 

对于 Visual Studio 中的 Python 项目，自定义环境会指定以下值，假定默认安装。

| 配置设置 | 值 |
|-----------------------|-------|
| **前缀路径** | C:\Program Files\Microsoft\PyForMLS |
| **解释器路径** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **窗口化解释器** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

<a name="create-iris-remotely"></a>

## <a name="optional-create-the-iris-database-remotely"></a>可选： 鸢尾花数据库远程创建

如果你有权在远程服务器上创建数据库，可以运行以下代码以创建用于本文中示例的鸢尾花演示数据库。

### <a name="1---create-the-irissql-database"></a>1-创建 irissql 数据库

```Python
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

### <a name="2---import-iris-sample-from-sklearn"></a>2-从导入鸢尾花示例 SkLearn

```Python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-recoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 RecoscalePy Api 来创建表并将鸢尾花数据加载

```Python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

<a name="install-ide"></a>

## <a name="next-steps"></a>后续步骤

现在，有工具和有效的连接到 SQL Server 的分步教程，以获取进一步了解 revoscalepy 函数和切换计算上下文。

> [!div class="nextstepaction"]
> [使用 revoscalepy 和远程计算上下文创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)