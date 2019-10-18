---
title: 为 R 开发设置数据科学客户端
description: 在开发工作站上安装本地 R 库和工具，以便远程连接到 SQL Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c81a69181d1bc723e622bac9ffeb5ff67fd0280
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "69633636"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>在 SQL Server 上为 R 开发设置数据科学客户端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

如果在[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或[SQL Server 机器学习服务（数据库内）](../install/sql-machine-learning-services-windows-install.md)安装中包括 r language 选项，则 r 集成在 SQL Server 2016 或更高版本中可用。 

若要为 SQL Server 开发和部署 R 解决方案，请在开发工作站上安装[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) ，以获取[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)和其他 R 库。 RevoScaleR 库在远程 SQL Server 实例上也是必需的，用于协调两个系统之间的计算请求。 

本文介绍如何配置 R 客户端开发工作站，以便能够与启用机器学习和 R 集成的远程 SQL Server 进行交互。 完成本文中的步骤后，你将拥有与 SQL Server 上的相同 R 库。 你还将了解如何将计算从本地 R 会话推送到 SQL Server 上的远程 R 会话。

![客户端-服务器组件](media/sqlmls-r-client-revo.png "本地和远程 R 会话与库")

若要验证安装，可以使用本文中所述的内置**rgui.exe**工具，或将[库链接](#install-ide)到通常使用的 RSTUDIO 或其他任何 IDE。

> [!Note]
> 客户端库安装的替代方法是使用[独立服务器](../install/sql-machine-learning-standalone-windows-install.md)作为丰富的客户端，而某些客户更喜欢更多的方案。 独立服务器与 SQL Server 完全分离，但由于它具有相同的 R 库，因此可以将它用作 SQL Server 数据库内分析的客户端。 你还可以将其用于非 SQL 相关的工作，包括从其他数据平台导入和建模数据的功能。 如果安装独立服务器，可以在以下位置找到 R 可执行文件： `C:\Program Files\Microsoft SQL Server\140\R_SERVER`。 若要验证安装，请[打开一个 r 控制台应用](#R-tools)，以便在该位置使用 ".exe" 运行命令。

## <a name="commonly-used-tools"></a>常用工具

无论你是 SQL 的 SQL 开发人员还是 R 和数据库内分析的 SQL 开发人员新手，都需要使用 R 开发工具和 T-sql 查询编辑器（如[SQL Server Management Studio （SSMS））](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)来执行数据库内的所有功能学.

对于简单的 R 开发方案，可以使用 RGUI.EXE 可执行文件，这些可执行文件捆绑在 MRO 和 SQL Server 中的基本 R 分发中。 本文介绍了如何将 RGUI.EXE 用于本地和远程 R 会话。 为了提高工作效率，应使用功能完备的 IDE，例如[RStudio 或 Visual Studio](#install-ide)。

SSMS 是一个单独的下载，适用于在 SQL Server 上创建和运行存储过程，包括包含 R 代码的存储过程。 您在开发环境中编写的几乎任何 R 代码都可以嵌入到存储过程中。 可以逐步执行其他教程，了解[SSMS 和 Embedded R](../tutorials/sqldev-in-database-r-for-sql-developers.md)。

## <a name="1---install-r-packages"></a>1-安装 R 包

Microsoft 的 R 包提供多种产品和服务。 在本地工作站上，我们建议安装 Microsoft R Client。 R 客户端提供[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)、 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)、 [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)和其他 R 包。

1. [下载 Microsoft R Client](https://aka.ms/rclient/download)。

2. 在安装向导中，接受或更改默认安装路径，接受或更改组件列表，并接受 Microsoft R Client 许可条款。

  安装完成后，欢迎屏幕将向你介绍产品和文档。

3. 创建 MKL_CBWR 系统环境变量，以确保在 Intel 数学内核库（MKL）计算上进行一致的输出。

  + 在控制面板中，单击 "**系统和安全** > **系统** > "**高级系统设置**" > **环境变量**"。
  + 创建一个名为**MKL_CBWR**的新系统变量，并将值设置为**AUTO**。

## <a name="2---locate-executables"></a>2-查找可执行文件

找到并列出安装文件夹的内容，确认已安装了 RGUI.EXE 和其他包。 

1. 在文件资源管理器中，打开 C:\Program Files\Microsoft\R Client\R_SERVER\bin 文件夹以确认 .exe 的位置。

2. 打开 x64 子文件夹以确认**rgui.exe**。 你将在下一步中使用此工具。

3. 打开 C:\Program Files\Microsoft\R Client\R_SERVER\library，查看随 R 客户端一起安装的包列表，包括 RevoScaleR、MicrosoftML 和其他。


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-启动 RGUI.EXE

在 SQL Server 中安装 R 时，将获得与 R 的任何基本安装标准相同的 R 工具，例如 Rgui.exe、Rterm.exe 等。 这些工具是轻型的，可用于检查包和库信息、运行即席命令或脚本，或者逐句通过教程。 可以使用这些工具获取 R 版本信息并确认连接。

1. 打开 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64，然后双击**rgui.exe**以使用 r 命令提示符启动 R 会话。

  从 Microsoft program 文件夹启动 R 会话时，会自动加载多个包，包括 RevoScaleR。 

2. 在命令提示符处输入 `print(Revo.version)` 以返回 RevoScaleR 包版本信息。 应为 RevoScaleR 使用版本9.2.1 或9.3.0。

3. 在 R 提示符下输入**search （）** 以获取已安装包的列表。

   ![加载 R 时的版本信息](../install/media/rclient-rgui-r-prompt.png "打开 R 提示符")


## <a name="4---get-sql-permissions"></a>4-获取 SQL 权限

在 R 客户端中，R 处理限制在两个线程和内存中的数据中。 对于使用多个核心和大型数据集的可缩放处理，可以将执行（称为*计算上下文*）转移到远程 SQL Server 实例的数据集和计算能力。 这是与生产 SQL Server 实例的客户端集成的建议方法，你将需要权限和连接信息来使其正常工作。

若要连接到 SQL Server 实例以运行脚本和上传数据，必须在数据库服务器上具有有效登录。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议你使用 Windows 集成身份验证，但对于某些方案，使用 SQL 登录更简单，特别是当你的脚本包含外部数据的连接字符串时。

用于运行代码的帐户至少必须具有读取正在处理的数据库的权限，以及执行任何外部脚本的特殊权限。 大多数开发人员还需要创建存储过程的权限，并将数据写入包含定型数据或评分数据的表中。 

要求数据库管理员在你使用 R 的数据库中为[你的帐户配置以下权限](../security/user-permission.md)：

+ **执行任何外部脚本**以在服务器上运行 R 脚本。
+ 用于运行用于定型模型的查询的**db_datareader**权限。
+ 用于编写定型数据或评分数据的**db_datawriter** 。
+ **db_owner**来创建存储过程、表和函数等对象。 
  还需要**db_owner**来创建示例数据库和测试数据库。 

如果你的代码需要 SQL Server 默认情况下未安装的包，请与数据库管理员一起将包与实例一起安装。 SQL Server 是一种受保护的环境，对包的安装位置有一些限制。 有关详细信息，请参阅[SQL Server 上的 "安装新的 R 包"](install-additional-r-packages-on-sql-server.md)。

## <a name="5---test-connections"></a>5-测试连接

 作为验证步骤，请使用**rgui.exe**和 RevoScaleR 确认到远程服务器的连接。 必须为[远程连接](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)启用 SQL Server，并且您必须具有权限，包括用户登录名和要连接到的数据库。 

以下步骤假定为 "演示数据库"、" [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)" 和 "Windows 身份验证"。

1. 在客户端工作站上打开**rgui.exe** 。 例如，请跳到 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`，然后双击 " **rgui.exe** " 以启动它。

2. RevoScaleR 自动加载。 通过运行以下命令确认 RevoScaleR 是否可操作： `print(Revo.version)`

3. 输入在远程服务器上执行的演示脚本。 必须修改以下示例脚本，使其包含远程 SQL Server 实例的有效名称。 此会话作为本地会话开始，但**rxSummary**函数在远程 SQL Server 实例上执行。

  ```R
  # Define a connection. Replace server with a valid server name.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
  # Specify the input data in a SQL query.
  sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
  # Define a remote compute context based on the remote server.
  cc <-RxInSqlServer(connectionString=connStr)

  # Execute the function using the remote compute context.
  rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
  ```

  **结果：**

  此脚本连接到远程服务器上的数据库，提供查询，创建计算上下文 `cc` 用于远程代码执行的指令，然后提供 RevoScaleR 函数**rxSummary**以返回查询结果的统计摘要。

  ```R
    Call:
  rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
      connectionString = connStr), computeContext = cc)

  Summary Statistics Results for: ~.
  Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
  Number of valid observations: 100 
  
  Name       Mean   StdDev   Min Max ValidObs MissingObs
  tip_amount 63.245 31.61087 36  180 100      0     
  ```

4. 获取并设置计算上下文。 设置计算上下文后，它在会话持续时间内保持有效。 如果不确定计算是本地的还是远程的，请运行以下命令来查找。指定连接字符串的结果表示远程计算上下文。

  ```R
  # Return the current compute context.
  rxGetComputeContext()

  # Revert to a local compute context.
  rxSetComputeContext("local")
  rxGetComputeContext()

  # Switch back to remote.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  cc <-RxInSqlServer(connectionString=connStr)
  rxSetComputeContext(cc)
  rxGetComputeContext()
  ```  

5. 返回有关数据源中的变量的信息，包括名称和类型。

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  结果包括23个变量。


6. 生成散点图以了解两个变量之间是否存在依赖关系。 

  ```R
  # Set the connection string. Substitute a valid server name for the placeholder.
  connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

  # Specify a query on the nyctaxi_sample table.
  # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
  sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
  cc <-RxInSqlServer(connectionString=connStr)

  # Generate a scatter plot.
  rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
  ```

  以下屏幕截图显示了输入和散点图输出。

   ![RGUI.EXE 中的散点图](media/rclient-setup-scatterplot.png "NYC 出租车演示数据的散点图")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-将工具链接到 R .exe

对于持续和严重的开发项目，您应安装集成开发环境（IDE）。 SQL Server 工具和内置 R 工具不适用于繁重的 R 开发。 一旦有了工作代码，就可以将其作为存储过程进行部署，以便在 SQL Server 上执行。

将 IDE 指向本地 R 库：基本 R、RevoScaleR 等。 脚本执行过程中运行工作 SQL Server 负荷时，如果脚本在 SQL Server 上调用远程计算上下文，则访问该服务器上的数据和操作。

### <a name="rstudio"></a>RStudio

当使用[RStudio](https://www.rstudio.com/)时，可以将环境配置为使用与远程 SQL Server 上的对应的 R 库和可执行文件。

1. 检查 SQL Server 上安装的 R 包版本。 有关详细信息，请参阅[获取 R 包信息](../package-management/r-package-information.md)。

1. 安装 Microsoft R Client 或一个独立的服务器选项来添加 RevoScaleR 和其他 R 包，包括 SQL Server 实例使用的基本 R 分发版。 选择同一级别或更低版本（包与后向兼容），提供与服务器上相同的包版本。 有关版本信息，请参阅本文中的版本映射：[升级 R 和 Python 组件](../install/upgrade-r-and-python.md)。

1. 在 RStudio 中，将[r 路径更新](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)为指向提供 RevoScaleR、Microsoft R Open 和其他 microsoft 包的 r 环境。 

  + 对于 R 客户端安装，请查看 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + 对于独立服务器，请查找 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 或 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. 关闭并打开 RStudio。

重新打开 RStudio 时，r 客户端（或独立服务器）上的 R 可执行文件是默认的 R 引擎。


### <a name="r-tools-for-visual-studio-rtvs"></a>针对 Visual Studio 的 R 工具（RTVS）

如果还没有适用于 R 的首选 IDE，则建议**针对 Visual Studio 的 R 工具**。

+ [下载针对 Visual Studio 的 R 工具（RTVS）](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [安装说明](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio)-RTVS 在多个版本的 Visual Studio 中提供。
+ [针对 Visual Studio 的 R 工具入门](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>从 RTVS 连接到 SQL Server

此示例使用安装了数据科学工作负荷的 Visual Studio 2017 社区版。

1. 从 "**文件**" 菜单中，选择 "**新建**"，然后选择 "**项目**"。

2. 左窗格包含预安装模板的列表。 单击 " **r**"，然后选择 " **r 项目**"。 在 "**名称**" 框中，键入 `dbtest` 然后单击 **"确定"** 。 

  Visual Studio 会创建一个新的项目文件夹和一个默认的脚本文件 `Script.R`。 

3. 在脚本文件的第一行键入 `.libPaths()`，然后按 CTRL + ENTER。

  当前 R 库路径应显示在**R 交互窗口**"窗口中。 

4. 单击 " **R 工具**" 菜单，然后选择 " **Windows** "，以查看可以在工作区中显示的其他 R 特定窗口的列表。
 
  + 通过按 CTRL + 3 查看当前库中有关包的帮助。
  + 通过按 CTRL + 8，查看**变量资源管理器**中的 R 变量。

## <a name="next-steps"></a>后续步骤

两个不同的教程包含练习，以便您可以练习将计算上下文从本地切换到远程 SQL Server 实例。

+ [教程：将 RevoScaleR R 函数与 SQL Server 数据结合使用](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)