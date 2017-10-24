---
title: "准备使用 PowerShell （演练） 的数据 |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1d85684da36ef69caf9dfa39f155a320def37b5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>准备使用 PowerShell （演练） 的数据

此时，应已安装下列项之一：

+ SQL Server 2016 R Services
+ SQL Server 自 2017 年 1 机器学习服务，与启用的 R 语言

在本课程中，你可以下载数据、 R 包和 R 脚本使用在本演练中，从 Github 存储库。 你可以下载所有内容为方便起见使用 PowerShell 脚本。

你还需要安装某些附加的 R 包，在服务器上和 R 工作站上。 介绍了的步骤。

然后，你可以使用第二个 PowerShell 脚本，RunSQL_R_Walkthrough.ps1，若要配置用于建模和评分的数据库。 脚本执行的数据大容量加载到数据库指定，然后创建一些 SQL 函数和简化数据科学任务的存储的过程。

让我们开始吧 ！

## <a name="1-download-the-data-and-scripts"></a>1.下载的数据和脚本

GitHub 存储库中提供了所需的所有代码。 可使用 PowerShell 脚本来创建文件的本地副本。

1.  在数据科学客户端计算机上，以管理员身份打开 Windows PowerShell 命令提示符。

2.  为确保可以运行下载脚本且不出错，请运行此命令。 该命令暂时允许脚本，而不会更改系统默认值。

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  运行以下 Powershell 命令，将脚本文件下载到本地目录。 如果不指定不同的目录，由默认文件夹`C:\tempR`创建和保存的所有文件。
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    如要将文件保存到另一个目录，请编辑参数 DestDir  的值，并在计算机上指定一个不同的文件夹。 如果你键入文件夹名称不存在，PowerShell 脚本将为您创建文件夹。
  
4.  下载可能需要花费一段时间。 下载完成后，Windows PowerShell 命令控制台应如下所示：
  
    ![完成 PowerShell 脚本后](media/rsql-e2e-psscriptresults.PNG "完成 PowerShell 脚本后")
  
5.  在 PowerShell 控制台中，可以运行命令 `ls` 查看下载到 DestDir 的文件列表。  文件的说明，请参阅[包含的内容](#What-the-Download-Includes)。

## <a name="2-install-required-r-packages"></a>2.安装所需的 R 程序包

本演练需要一些未默认作为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]的一部分安装的 R 库。 你必须在客户端上安装这两个包，在开发解决方案，和上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将解决方案部署的计算机。

### <a name="install-required-packages-on-the-client"></a>在客户端上安装所需的包

下载的 R 脚本包括下载和安装这些包的命令。

1. 在 R 环境中，打开脚本文件 RSQL_R_Walkthrough.R。

2. 突出显示并执行这些行。
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    某些包还安装所需的程序包。 总共大约需要 32 个包。

### <a name="install-required-packages-on-the-server"></a>在服务器上安装所需的包

有多种不同的方法，你可以在 SQL Server 上安装包。 例如，SQL Server 提供[包管理](../r/installing-and-managing-r-packages.md)功能，它允许数据库管理员创建的程序包存储库并将用户分配的权限来安装其自己的程序包。 但是，如果你是计算机上的管理员，你可以安装使用 R，新包，只要您将安装到正确的库。

> [!NOTE]
> 在服务器上，**不这样做**即使提示安装到用户的库。 若要安装到用户库时，SQL Server 实例无法找到或运行包。 有关详细信息，请参阅 [在 SQL Server 上安装新的 R 包](../r/install-additional-r-packages-on-sql-server.md)。

1. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上，**以管理员身份**打开 RGui.exe。  如果已使用默认值安装 SQL Server R Services，则可以在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64) 中找到 RGui.exe。

2.  在 R 提示符处，运行下面的 R 命令：
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - 此示例使用 R grep 函数搜索可用路径的向量，并在“Program Files”中找到一个。 有关详细信息，请参阅 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)。

    - 如果您认为程序包都已安装，请通过运行检查安装程序包的列表`installed.packages()`。

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3.准备使用 RunSQL_R_Walkthrough.ps1 的环境

数据文件、 R 脚本和 T-SQL 脚本中，以及下载内容还包括 PowerShell 脚本`RunSQL_R_Walkthrough.ps1`。 该脚本执行以下操作：

- 检查是否已安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQL Native Client 和命令行实用程序。 需要命令行工具才能运行 [bcp 实用工具](../../tools/bcp-utility.md)，此实用工具用于将批量数据快速加载到 SQL 表。

- 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例，并运行某些配置数据库以及创建模型和数据的表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。

- 运行 SQL 脚本，创建多个存储过程。

- 将前面下载的数据加载到名为 `nyctaxi_sample` 的表中。

- 重写 R 脚本文件中的参数，以使用指定的数据库名称。

你应运行此脚本的计算机上生成解决方案的位置： 例如，便携式计算机开发和测试 R 代码。 此计算机（称为数据科学客户端）必须能够使用命名管道协议连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机。

1. 打开 PowerShell 命令行**以管理员身份**。
  
2.  导航到下载这些脚本的文件夹，并键入如下所示的脚本名称。 按 Enter。

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  系统提示您为每个以下参数：
  
    **数据库服务器名称**： 机器学习服务或 R Services 的安装位置的 SQL Server 实例的名称。

    根据网络的要求，实例名称可能需要具有一个或多个子网名称的限定。  例如，如果 MYSERVER 不起作用，请尝试使用 myserver.subnet.mycompany.com。
    
    **要创建的数据库的名称**：例如，可以键入 **Tutorial** 或 **Taxi**

    **用户名**：提供拥有数据库访问特权的帐户。 存在两个选项：
    
    + 键入具有“创建数据库”权限的 SQL 登录名，然后在后续提示符处提供 SQL 密码。
    + 无需键入任何名称，只需按 Enter 使用自己的 Windows 标识，然后在安全提示符下键入 Windows 密码。 PowerShell 不支持输入其他 Windows 用户名。
    + 如果你没有指定有效的用户，该脚本将默认为使用集成的 Windows 身份验证。
    
      > [!WARNING]
      > 时使用 PowerShell 脚本中的提示，提供你的凭据，则会将密码写入纯文本中的更新的脚本文件。 创建所需的 R 对象后，请立即编辑该文件以删除凭据。
      
    **csv 文件的路径**：提供数据文件的完整路径。 默认路径和文件名为 `C:\tempR\nyctaxi1pct.csv1`。
  
4.  按 Enter 运行该脚本。

    脚本应会下载文件，并自动将数据加载到数据库中。 这可能需要一段时间。 查看 PowerShell 窗口中的状态消息。
      
    如果大容量导入或任何其他步骤失败，你可以将数据加载手动中所述[故障排除](#bkmk_Troubleshooting)部分。

**结果（成功完成）**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

单击此链接可跳转到下一课：[视图和浏览使用 SQL 数据](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>故障排除

如果你有 PowerShell 脚本中的任何问题，你可以全部或任意步骤手动运行，作为示例使用 PowerShell 脚本的行。 本部分列出了一些常见的问题和解决方法。

### <a name="powershell-script-didnt-download-the-data"></a>PowerShell 脚本未下载数据

若需手动下载数据，请右键单击下面的链接，然后选择“目标另存为” 。

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

记下已下载的数据文件的路径以及保存有数据的文件的文件名。 你需要将数据加载到表使用的完整路径**bcp**。

### <a name="unable-to-download-the-data"></a>无法下载数据

数据文件过大。 你必须使用的计算机具有相对较好的 Internet 连接，或下载可能会超时。

### <a name="could-not-connect-or-script-failed"></a>无法连接或脚本失败

运行某个脚本时可能会出现以下错误：“与 SQL Server 建立连接时发生了与网络相关的或特定于实例的错误”

+ 检查实例名称的拼写。
+ 验证是否是完整的连接字符串。
+ 根据网络的要求，实例名称可能需要具有一个或多个子网名称的限定。  例如，如果 MYSERVER 不起作用，请尝试使用 myserver.subnet.mycompany.com。
+ 检查 Windows 防火墙是否允许通过 SQL Server 的连接。
+ 尝试注册服务器，确保服务器允许远程连接。
+ 如果使用命名实例，请启用 SQL 浏览器以方便建立连接。

### <a name="network-error-or-protocol-not-found"></a>网络错误或者找不到协议

+ 验证该实例是否支持远程连接。
+ 验证指定的 SQL 用户是否可以远程连接到数据库。
+ 在实例上启用命名管道。
+ 检查帐户权限。 指定的帐户可能不具有创建新的数据库和上传数据的权限。

### <a name="bcp-did-not-run"></a>bcp 未运行

+ 验证 [bcp 实用工具](../../tools/bcp-utility.md) 在计算机上是否可用。 可从 PowerShell 窗口或 Windows 命令提示符运行 **bcp**。
+ 如果出现错误，请将 **bcp** 实用工具的位置添加到 PATH 系统环境变量，然后重试。

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>已创建表架构，但表中没有数据

如果脚本的其余部分运行正常，可从命令行调用 **bcp** ，将数据手动上传到表中，如下所示：

#### <a name="using-a-sql-login"></a>使用 SQL 登录名

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>使用 Windows 身份验证

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ `in`关键字指定数据移动的方向。
+ 参数  **-f** 要求指定格式文件的完整路径。 如果使用 **in** 选项，则需格式文件。
+ 如果要通过 SQL 登录名运行 bcp，请使用 **-U** 和 **-P** 参数。
+ 如果要使用 Windows 集成身份验证，请使用 **-T** 参数。

如果脚本未加载数据，请检查语法，并确认是否为网络正确指定了服务器名称。 例如，若要连接到命名实例，请务必包含所有子网和计算机名称。 验证的登录帐户具有执行大容量上载的能力。

### <a name="i-want-to-run-the-script-without-prompts"></a>我希望在无提示的情况下运行脚本

可以在此模板中使用特定于环境的值，通过单个命令行指定所有参数。

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

以下示例使用 SQL 登录名运行脚本：

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   使用 SqlUserName 的凭据连接到指定的实例和数据库。
-   获取文件 C:\temp\nyctaxi1pct.csv 中的数据。
-   在名为 MyServer 的 *实例上，将数据加载到数据库 MyDB*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的表 dbo.nyctaxi_sample 。

### <a name="the-data-loaded-but-it-contains-duplicates"></a>数据已加载，但包含重复项

如果你的数据库包含现有表的相同的名称和相同的架构， **bcp**插入的数据而不是覆盖现有数据的新副本。

若要避免重复数据，请截断所有现有的表，然后重新运行脚本。

## <a name="whats-included-in-the-sample"></a>在此示例中包含的内容

当你从 GitHub 存储库下载文件时，可以获得以下：

+ 采用 CSV 格式; 数据请参阅[训练和评分数据](#bkmk_data)有关详细信息
+ 用于准备环境的 PowerShell 脚本
+ 用于通过 bcp 将数据导入到 SQL Server 中的 XML 格式文件
+ 多个 T-SQL 脚本
+ 运行此演示所需的所有 R 代码

### <a name="bkmk_data"></a>定型集和评分的数据

该数据是纽约市出租车数据集的一个代表样本，其包含 2013 年逾 1.73 亿次单个行程的记录，包括每次行程支付的车费和小费。 为更轻松地使用数据，Microsoft 数据科学团队进行了缩小取样，仅获取 1% 的数据。  此数据已以 CSV 格式共享在 Azure 中的公共 Blob 存储容器中。 源数据是未压缩的文件，低于 350 MB。

+ 公共数据集: [NYC Taxi 和 Limousine 佣金] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [NYC Taxi 数据集上生成 Azure ML 模型](https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/。

### <a name="powershell-and-r-script-files"></a>PowerShell 和 R 脚本文件

+ **RunSQL_R_Walkthrough.ps1**运行此脚本首先，使用 PowerShell。 这将调用 SQL 脚本，将数据加载到数据库中。

+ **taxiimportfmt.xml** ：BCP 实用工具用来将数据加载到数据库的格式定义文件。

+ **RSQL_R_Walkthrough.R**这是在执行数据分析和建模课程的其余部分中使用的核心 R 脚本。 该脚本提供浏览 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据、生成分类模型和创建绘图需要的所有 R 代码。

### <a name="t-sql-script-files"></a>T-SQL 脚本文件

执行 PowerShell 脚本的多个[!INCLUDE[tsql](../../includes/tsql-md.md)]SQL Server 实例上的脚本。 下表列出[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本和它们执行的操作。

|SQL 脚本文件名|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|创建数据库和两个表：<br /><br /> ：存储定型数据（即纽约市出租车数据集 1% 样本）的表。 将在表中添加一个聚集列存储索引，改善存储和查询性能。<br /><br /> ：稍后会用于保存已定型的分类模型的空表。|
|PredictTipBatchMode.sql|创建一个存储过程，用于调用已定型的模型预测新观测值的标签。 该存储过程接受查询作为其输入参数。|
|PredictTipSingleMode.sql|创建一个存储过程，用于调用已定型的分类模型预测新观测值的标签。 传入的新观测值的变量作为嵌入式参数。|
|PersistModel.sql|创建一个存储过程，用于帮助在数据库的表中存储分类模型的二进制表示形式。|
|fnCalculateDistance.sql|创建一个 SQL 标量值函数，用于计算搭乘位置和下车位置之间直接距离。|
|fnEngineerFeatures.sql|创建一个 SQL 表值函数，该函数可创建用于定型分类模型的功能|

本演练中使用的 T-SQL 查询已经过测试并可以作为运行-在 R 代码。 但是，如果你想要进一步试验或开发自己的解决方案，我们建议先使用专用的 SQL 开发环境来测试并优化查询，然后将其添加到 R 代码。

+ 适用于 [Visual Studio Code](https://code.visualstudio.com/) 的 [mssql 扩展](https://code.visualstudio.com/docs/languages/tsql)是一个免费的轻型环境，用于运行同样支持大多数数据库开发任务的查询。
+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 是一个功能强大的免费工具，用于开发和管理 SQL Server 数据库。

## <a name="next-lesson"></a>下一课

[查看和浏览使用 R 和 SQL 的数据](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>上一课

[R 和 SQL Server 的端到端数据科学演练](/walkthrough-data-science-end-to-end-walkthrough.md)

[数据科学演练的先决条件](walkthrough-prerequisites-for-data-science-walkthroughs.md)

