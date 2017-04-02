---
title: "第 1 课：准备数据（数据科学端到端演练） | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# 第 1 课：准备数据（数据科学端到端演练）
为准备此演练，需要执行以下操作：

1. 下载演练中要使用的数据和所有 R 脚本。 提供 PowerShell 脚本以简化从 GitHub 的下载。   

2. 在服务器和 R 工作站上安装一些其他的 R 包。  

3. 准备环境，包括用于建模和计分的数据库和数据。
 
    为此，需要使用另一个 PowerShell 脚本 RunSQL_R_Walkthrough.ps1。
    该脚本可配置数据库，并将数据上传到指定的表。  它还会创建一些可简化数据科学任务的 SQL 函数和存储过程。 
 

## <a name="1-download-the-data-and-scripts"></a>1.下载数据和脚本  
GitHub 存储库中提供了完成本演练所需的所有代码。 可使用 PowerShell 脚本来创建文件的本地副本。  
  
#### <a name="to-download-all-scripts-using-powershell"></a>使用 PowerShell 下载所有脚本  
  
1.  在数据科学客户端计算机上，以管理员身份打开 Windows PowerShell 命令提示符。  
  
2.  如果之前未在此实例上运行过 PowerShell，或没有运行脚本的权限，可能会遇到错误。 如果是这种情况，请在运行该脚本之前先运行此命令，这样便可在不更改系统默认值的情况下暂时允许运行脚本。  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  运行以下命令，将脚本文件下载到本地目录。 如果不指定另一个目录，则默认情况下，将创建文件夹 C:\tempR 并将所有文件保存其中。  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    如要将文件保存到另一个目录，请编辑参数 DestDir 的值，并在计算机上指定一个不同的文件夹。 如果键入的文件夹名不存在，PowerShell 脚本将创建该文件夹。  
  
4.  下载完成后，Windows PowerShell 命令控制台应如下所示：  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  在 PowerShell 控制台中，可以运行命令 `ls` 查看下载到 DestDir 的文件列表。  有关文件列表和文件说明，请参阅[包含内容](#What-the-Download-Includes)。
  
## <a name="2-install-required-packages"></a>2.安装所需的包  
本演练需要一些未默认作为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的一部分安装的 R 库。 必须将这些包安装到将在其中开发解决方案的客户端上以及将在其中部署解决方案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上。  
  
### <a name="install-required-packages-on-the-client"></a>在客户端上安装所需的包  
下载的 R 脚本包括下载和安装这些包的命令。  
  
1.  在 R 环境中，打开脚本文件 RSQL_R_Walkthrough.R。  
  
2.  突出显示并执行这些行。  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>在服务器上安装所需的包  

  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上，以管理员身份打开 RGui.exe。  如果已使用默认值安装 SQL Server R Services，则可以在 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64) 中找到 RGui.exe。  
  
    或者，如果已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上安装了另一个 R 环境（例如 RStudio），则可以使用 R 控制台运行命令。  
  
2.  在 R 提示符处，运行下面的 R 命令：  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**说明：**  
  
-   此示例使用 R grep 函数搜索可用路径的向量，并在“Program Files”中找到一个。 有关详细信息，请参阅 [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep)。   
  
-   如果认为包已安装，请使用 R 函数 `installed.packages()` 查看已安装包的列表。  
  
-   在客户端上，如果无法写入到“Program Files”中的主库，则可安装到用户库。 但是，将包安装到 SQL Server 计算机时，必须将其安装到 SQL Server R Services 所使用的默认库中。 不要使用用户库。 有关详细信息，请参阅[在 SQL Server 上安装新的 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)。
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3.运行 PowerShell 脚本 RunSQL_R_Walkthrough.ps1  

可以在用于生成解决方案的计算机上运行此 PowerShell 脚本，例如，用于开发和测试 R 代码的计算机。 此计算机必须能够使用命名管道协议连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机。  
  
该脚本执行以下操作：  
  
-   检查是否已安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQL Native Client 和命令行实用程序。 需要命令行工具才能运行 [bcp 实用工具](../../tools/bcp-utility.md)此实用工具用于将大容量数据快速加载到 SQL 表。    
-   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的指定实例，并运行某些配置数据库以及创建模型和数据的表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。    
-   运行 SQL 脚本，创建多个存储过程。    
-   将之前下载的数据加载到表 nyctaxi_sample。    
-   重写 R 脚本文件中的参数，以使用指定的数据库名称。 

### <a name="to-run-the-script"></a>运行该脚本
  
1.  以管理员身份打开 PowerShell 命令行。    
  
2.  导航到下载这些脚本的文件夹，并键入如下所示的脚本名称。 按 Enter。  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  系统将提示以下每个参数：  
  
    - 要创建的数据库的名称。 
      例如，可键入**教程**或**出租车**  
    - 运行脚本所依据的凭据。 存在两个选项：
        + 键入具有“创建数据库”权限的 SQL 登录名，然后在后续提示符处提供 SQL 密码。
        + 无需键入任何名称，只需按 Enter 使用自己的 Windows 标识，然后在安全提示符处，键入 Windows 密码。 PowerShell 不支持输入其他 Windows 用户名。 

          如果未能指定有效的用户，则该脚本默认会使用集成的 Windows 身份验证。  
  
    -   要上传到数据库的 csv 文件的完整路径  
  
        脚本应自动下载文件，并将数据加载到数据库，但如果此操作失败，可以随时手动上传数据。  
  
4.  按 Enter 运行该脚本。  
  
## <a name="troubleshooting"></a>故障排除  
 
 若遇到问题，可手动运行所有或任何步骤，以此 PowerShell 脚本行作为示例。 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>该 PowerShell 脚本未下载数据
  
若需手动下载数据，请右键单击下面的链接，然后选择“目标另存为”。  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
记下已下载的数据文件的路径以及保存有数据的文件的文件名。 使用 **bcp**将数据加载到表时会用到此路径。  
  
### <a name="i-was-unable-to-download-the-data"></a>无法下载数据
数据文件过大。 请使用 Internet 连接相对较好的计算机，否则下载可能会超时。  

  
### <a name="could-not-connect-or-script-failed"></a>无法连接或脚本失败  
  
+ 检查实例名称的拼写。 
+ 验证是否是完整的连接字符串。    
+ 根据网络的要求，实例名称可能需要具有一个或多个子网名称的限定。  例如，如果 MYSERVER 不起作用，请尝试使用 myserver.subnet.mycompany.com。
  
### <a name="network-error-or-protocol-not-found"></a>网络错误或者找不到协议  
  
+ 验证该实例是否支持远程连接。    
+ 验证指定的 SQL 用户是否可以远程连接到数据库，以及是否在实例上启用了命名管道。    
+ 检查帐户权限。 指定的帐户可能不具有创建新的数据库和上传数据的权限。  

### <a name="bcp-did-not-run"></a>bcp 未运行  

+ 验证 [bcp 实用工具](../../tools/bcp-utility.md) 在计算机上是否可用。 可从 PowerShell 窗口或从 Windows 命令提示符处运行 bcp。
+ 如果出现错误，将 bcp 实用工具的位置添加到 PATH 系统环境变量，然后重试。  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>已创建表架构，但表中没有数据

如果脚本的其余部分运行正常，可从命令行调用 **bcp**，将数据手动上传到表中，如下所示：  


 
**使用 SQL 登录名**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**使用 Windows 身份验证**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ 关键字 **in** 指定数据移动的方向。  
+ 参数 **-f** 要求指定格式文件的完整路径。 如果使用 **in** 选项，则需格式文件。
+ 如果要通过 SQL 登录名运行 bcp，请使用 **-U** 和 **-P** 参数。
+ 如果要使用 Windows 集成身份验证，请使用 **-T**参数。 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>如何在无提示的情况下运行此脚本？  
  
可使用特定于环境的值，在单个命令行中指定所有参数。 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
例如，使用 SQL 登录名运行脚本：  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
此示例将执行下列操作：  
  
-   使用 SqlUserName 的凭据连接到指定的实例和数据库。  
-   获取文件 C:\temp\nyctaxi1pct.csv 中的数据。  
-   在名为 MyServer 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上，将数据加载到数据库 MyDB 中的表 dbo.nyctaxi_sample。  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>数据已加载，但包含重复项

如果存在现有的表，并且表的架构正确，则 bcp 将继续运行，但不会覆盖现有数据，而是插入数据的新副本。 这将导致出现重复数据。  重新运行此脚本前，请务必截断现有表。

## <a name="what-the-download-includes"></a>下载内容

从 GitHub 存储库下载的文件包括：
+ CSV 格式的数据
+ 用于准备环境的 PowerShell 脚本
+ 用于通过 bcp 将数据导入到 SQL Server 中的 XML 格式文件
+ 多个 T-SQL 脚本
+ 运行此演示所需的所有 R 代码

### <a name="training-and-scoring-data"></a>定型数据和计分数据  
该数据是纽约市出租车数据集的一个代表样本，其包含 2013 年逾 1.73 亿次单个行程的记录，包括每次行程支付的车费和小费。  有关此数据是如何原样收集以及如何获取完整数据集的详细信息，请参阅  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/)。  
  
为更轻松地使用数据，Microsoft 数据科学团队进行了缩小取样，仅获取 1% 的数据。  此数据已以 CSV 格式共享在 Azure 中的公共 Blob 存储容器中。 源数据是未压缩的文件，低于 350 MB。  
 
### <a name="files"></a>“文件”

 
+ **RunSQL_R_Walkthrough.ps1**：首先，使用 PowerShell 运行此脚本。 这将调用 SQL 脚本，将数据加载到数据库中。  
    
+ **taxiimportfmt.xml**：BCP 实用工具用来将数据加载到数据库的格式定义文件。
      
+ **RSQL_R_Walkthrough.R**：这是其余课程中用于数据分析和建模的核心 R 脚本。 该脚本提供浏览 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据、生成分类模型和创建绘图需要的所有 R 代码。   
  
### <a name="sql-scripts"></a>SQL 脚本  
此 PowerShell 脚本在服务器上执行多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 下表列出了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。  
  
|SQL 脚本文件名|作用|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|创建数据库和两个表：<br /><br /> nyctaxi_sample：存储定型数据（即纽约市出租车数据集 1% 样本）的表。 将在表中添加一个聚集列存储索引，改善存储和查询性能。<br /><br /> nyc_taxi_models：稍后会用于保存已定型的分类模型的空表。|  
|PredictTipBatchMode.sql|创建一个存储过程，用于调用已定型的模型预测新观测值的标签。 该存储过程接受查询作为其输入参数。|  
|PredictTipSingleMode.sql|创建一个存储过程，用于调用已定型的分类模型预测新观测值的标签。 传入的新观测值的变量作为嵌入式参数。|  
|PersistModel.sql|创建一个存储过程，用于帮助在数据库的表中存储分类模型的二进制表示形式。|  
|fnCalculateDistance.sql|创建一个 SQL 标量值函数，用于计算搭乘位置和下车位置之间直接距离。|  
|fnEngineerFeatures.sql|创建一个 SQL 表值函数，该函数可创建用于定型分类模型的功能|  
  
本演练中使用的所有 SQL 查询都已经过测试并可在 R 代码中原样运行。 但是，如果想要进一步试验或使用 SQL 查询开发自己的解决方案，建议使用如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 这样的开发环境，先对查询进行测试和调整，再将其添加到 R 代码。  
  
  
## <a name="next-lesson"></a>下一课  
[第 2 课：查看和浏览数据（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[数据科学端到端演练](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  
