---
title: 设置 Python 开发的 SQL Server 机器学习数据科学客户端
description: 设置远程连接到 SQL Server 机器学习服务与 Python 配合使用 Python 在本地环境 （Jupyter Notebook 或 PyCharm）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6c302f7cc9830b15ed058c160618ea0e40705444
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962737"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>设置 SQL Server 机器学习服务的 Python 开发数据科学客户端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 集成是可用时包括中的 Python 选项启动 SQL Server 2017 或更高版本[机器学习服务 （数据库） 安装](../install/sql-machine-learning-services-windows-install.md)。 

若要开发和部署适用于 SQL Server Python 解决方案时，安装 Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)和其他 Python 库在开发工作站。 Revoscalepy 库，也是远程的 SQL Server 实例上，可协调计算这两个系统之间的请求。 

在本文中，了解如何配置 Python 开发工作站，以便您可以使用远程 SQL Server 启用了机器学习和 Python 集成进行交互。 完成这篇文章中的步骤后，将具有与 SQL Server 上的相同 Python 库。 此外将了解如何在 SQL Server 上推送到远程的 Python 会话从本地 Python 会话计算。

![客户端-服务器组件](media/sqlmls-python-client-revo.png "本地和远程 Python 会话和库")

若要验证安装，可以使用内置的 Jupyter 笔记本，这篇文章中所述或[链接库](#install-ide)PyCharm 或任何你通常使用的另一个 IDE。

> [!Tip]
> 这些练习的视频演示，请参阅[运行 R 和 Python 在 Jupyter Notebook 从 SQL Server 中远程](https://youtu.be/D5erljpJDjE)。

> [!Note]
> 客户端库安装的替代方法是使用[独立服务器](../install/sql-machine-learning-standalone-windows-install.md)作为富客户端，一些客户更喜欢使用它来完成更深入的方案工作。 从 SQL Server 完全分离的独立服务器，但因其具有相同的 Python 库，你可以使用它作为客户端的 SQL Server 数据库内分析。 还可以将其用于与SQL无关的工作，包括从其他数据平台导入数据和对数据建模。 如果安装在独立服务器，可以找到在此位置的 Python 可执行文件： `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`。 若要验证你的安装，[打开 Jupyter notebook](#python-tools)以使用 Python.exe，在该位置运行命令。

## <a name="commonly-used-tools"></a>常用工具

无论您是熟悉 SQL，在 Python 开发人员或 SQL 开发人员首次使用 Python 和数据库内分析，您将需要 Python 开发工具和 T-SQL 查询编辑器等[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)以实现所有数据库内分析功能。

对于 Python 开发，可以使用 Jupyter 笔记本，这在 SQL Server 安装的 Anaconda 分发版捆绑。 本文介绍如何启动 Jupyter Notebook，以便您可以运行 Python 代码本地和远程 SQL 服务器上。

SSMS 是单独的下载，适用于创建和运行 SQL Server，包括那些包含 Python 代码上的存储的过程。 可以在存储过程中嵌入几乎任何在 Jupyter 笔记本中编写的 Python 代码。 你可以逐步浏览其他快速入门，了解如何[SSMS 和嵌入式的 Python](../tutorials/quickstart-python-verify.md)。

## <a name="1---install-python-packages"></a>1-安装 Python 包

本地工作站必须具有与 SQL Server，包括基本 Anaconda 4.2.0 与 Python 3.5.2 分发和特定于 Microsoft 的包上的相同 Python 包版本。

安装脚本将三个特定于 Microsoft 的库添加到 Python 客户端。 该脚本将安装[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)，用于定义数据源对象和计算上下文。 它将安装[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)提供机器学习算法。 [Azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk)还安装包，但它适用于与独立 （非实例） 的机器学习服务器上下文关联的操作化任务并且可能会限制使用的数据库内分析。

1. 下载安装脚本。

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) 安装版本 9.2.1 Microsoft Python 程序包。 此版本对应于默认 SQL Server 2017 实例。 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 安装版本 9.3 的 Microsoft Python 包。 此版本是更好的选择，如果远程 SQL Server 2017 实例[绑定到机器学习服务器 9.3](../install/upgrade-r-and-python.md)。

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

仍在 PowerShell 中，列出要确认安装了 Python.exe、 脚本和其他包的安装文件夹的内容。 

1. 输入`cd \`以转到根驱动器，然后输入为指定的路径`-InstallFolder`在上一步。 如果在安装过程中省略此参数，默认值是`cd C:\Program Files\Microsoft\PyForMLS`。

2. 输入`dir *.exe`若要列出可执行文件。 应会看到**python.exe**， **pythonw.exe**，并**卸载 anaconda.exe**。

  ![Python 可执行文件的列表](media/powershell-python-exe.png)
   
在系统上将多个版本的 Python，请记住如果您想要加载，请使用此特定 Python.exe **revoscalepy**和其他 Microsoft 包。

> [!Note] 
> 安装脚本不会修改你在计算机上，这意味着新的 python 解释器和您刚刚安装的模块不自动提供给可能有其他工具的 PATH 环境变量。 将 Python 解释器和库链接到工具的帮助，请参阅[安装 IDE](#install-ide)。

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-打开 Jupyter Notebook

Anaconda 包含的 Jupyter 笔记本。 下一步，创建一个 notebook 并运行包含您刚安装的库的某些 Python 代码。

1. 在 Powershell 提示符下，仍在 C:\Program Files\Microsoft\PyForMLS 目录中，打开 Jupyter Notebook 从脚本文件夹中：

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  应该在默认浏览器中打开笔记本`https://localhost:8889/tree`。

  启动另一种方法是双击**jupyter notebook.exe**。 

2. 单击**新建**，然后单击**Python 3**。

  ![使用新的 Python 3 选择的 jupyter 笔记本](media/jupyter-notebook-new-p3.png)

3. 输入`import revoscalepy`并运行到加载特定于 Microsoft 的库的命令。

4. 输入并运行`print(revoscalepy.__version__)`要返回的版本信息。 应会看到 9.2.1 或 9.3.0。 可以使用与这些版本之一[服务器上的 revoscalepy](../package-management/installed-package-information.md)。 

4. 输入一系列更复杂的语句。 此示例生成汇总统计信息使用[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)对本地数据集。 其他函数获取示例数据的位置，并创建本地.xdf 文件的数据源对象。

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

以下屏幕截图显示的输入和输出中，已简化的一部分。

  ![显示 revoscalepy 输入和输出的 jupyter 笔记本](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-获取 SQL 权限

若要连接到要运行脚本和上传数据的 SQL Server 实例，必须在数据库服务器上具有有效的登录名。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议使用 Windows 集成身份验证，但使用 SQL 登录名是在某些情况下，更简单，尤其是在脚本中包含对外部数据连接字符串时。

最小值，用来运行代码的帐户必须具有你正在使用，加上特殊权限执行任意外部脚本从数据库中读取的权限。 大多数开发人员还需要权限才能创建存储的过程，并将数据写入到包含训练数据的表或评分的数据。 

询问数据库管理员来[配置你的帐户的以下权限](../security/user-permission.md)，其中使用 Python 在数据库中：

+ **EXECUTE ANY EXTERNAL SCRIPT**若要在服务器上运行 Python。
+ **db_datareader**权限才能运行用于定型模型的查询。
+ **db_datawriter**编写定型数据或评分的数据。
+ **db_owner**以创建对象的存储过程，如表、 函数。 
  您还需要**db_owner**创建示例，并测试数据库。 

如果你的代码需要与 SQL Server 的默认情况下不安装的程序包，排列与数据库管理员能够与实例安装的包。 SQL Server 是一个受保护的环境并在其中安装包的限制。 不建议临时安装的包作为你的代码的一部分，即使您具有权限。 此外，server 库中安装新包之前始终仔细考虑的安全隐患。


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-创建测试数据

如果你有权在远程服务器上创建数据库，可以运行以下代码以创建用于在本文的剩余步骤的鸢尾花演示数据库。

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

### <a name="2---import-iris-sample-from-sklearn"></a>2-从导入鸢尾花示例 SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-使用 Revoscalepy Api 来创建表并将鸢尾花数据加载

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-测试远程连接

此下一步之前，请确保您具有 SQL Server 实例和连接字符串上的权限[鸢尾花示例数据库](../tutorials/demo-data-iris-in-sql.md)。 如果数据库不存在并且具有足够的权限，则可以[使用这些内联说明创建数据库](#create-iris-remotely)。

连接字符串替换为有效的值。 示例代码使用`"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`，但你的代码应具有一个实例的名称，并映射到数据库用户登录名的凭据选项可能指定远程服务器。

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


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-从工具启动 Python

因为开发人员经常使用多个版本的 Python，安装程序不向路径添加 Python。 若要使用的 Python 可执行文件和由安装程序安装的库，链接到你的 IDE **Python.exe**还提供的路径处**revoscalepy**并**microsoftml**。 

### <a name="command-line"></a>命令行

在运行时**Python.exe**从 C:\Program Files\Microsoft\PyForMLS （或 Python 客户端库安装指定的任何位置），您可以访问完整的 Anaconda 分发版加上 Microsoft Python模块， **revoscalepy**并**microsoftml**。

1. 转到 C:\Program Files\Microsoft\PyForMLS 并双击**Python.exe**。
2. 打开交互式帮助： `help()`
3. 帮助提示符处键入的模块的名称： `help> revoscalepy`。 帮助返回名称、 包的内容、 版本和文件位置。
4. 返回在版本和包信息**帮助 >** 提示符： `revoscalepy`。 按 Enter 几次以退出帮助。
5. 导入模块： `import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter 笔记本

本文使用内置的 Jupyter Notebook 演示对函数调用**revoscalepy**。 如果您不熟悉此工具，以下屏幕截图演示了部分的结合方式和原因一切正常。 

父文件夹 C:\Program Files\Microsoft\PyForMLS 包含 Anaconda 以及 Microsoft 包。 Jupyter 笔记本包含在 Anaconda，在脚本文件夹中，Python 可执行文件不自动注册使用 Jupyter Notebook。 在 site-packages 下找到包可以导入到的笔记本，包括用于数据科学和机器学习的三个 Microsoft 包中。

  ![可执行文件和库](media/jupyter-notebook-python-registration.png)

如果使用的另一个 IDE，您需要将 Python 可执行文件和函数库链接到所需的工具。 以下部分提供的常用工具的说明。

### <a name="visual-studio"></a>Visual Studio

如果有[Visual Studio 中的 Python](https://code.visualstudio.com/docs/languages/python)，使用以下配置选项来创建包含 Microsoft Python 包的 Python 环境。

| 配置设置 | value |
|-----------------------|-------|
| **前缀路径** | C:\Program Files\Microsoft\PyForMLS |
| **解释器路径** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **窗口化解释器** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

为了帮助您配置的 Python 环境，请参阅[Visual Studio 中的管理 Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

### <a name="pycharm"></a>PyCharm

集中 PyCharm，由机器学习服务器安装到 Python 可执行文件的解释器。

1. 在新项目中，在设置中，单击**添加本地**。

2. 输入`C:\Program Files\Microsoft\PyForMLS\`。

现在，你可以导入**revoscalepy**， **microsoftml**，或**azureml**模块。 你还可以选择**工具** > **Python 控制台**打开交互窗口。

## <a name="next-steps"></a>后续步骤

现在，有工具和有效的连接到 SQL Server，通过运行通过 Python 快速入门使用扩展你的技能[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

> [!div class="nextstepaction"]
> [快速入门：验证存在 SQL Server 中的 Python](../tutorials/quickstart-python-verify.md)