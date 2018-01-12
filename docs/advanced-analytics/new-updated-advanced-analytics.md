---
title: "更新-为 SQL Server 文档高级分析 |Microsoft 文档"
description: "显示更新内容的最近更改中的文档，为 Microsoft SQL server 的高级分析的代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2017
ms.author: genemi
ms.workload: 
ms.openlocfilehash: 65bdb7f8f8547644d6c8b32606e17c18983aa717
ms.sourcegitcommit: 06131936f725a49c1364bfcc2fccac844d20ee4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新的和最近的更新： SQL Server 的高级分析



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- *主题区域：* &nbsp; **for SQL Server 的高级分析**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


1. [将 SQLRUserGroup 添加为数据库用户](r/add-sqlrusergroup-to-database.md)
2. [如何使用 RevoScaleR 函数来查找或在 SQL Server 上安装 R 包](r/use-revoscaler-to-manage-r-packages.md)
3. [在 Azure SQL Database 中使用 R](r/using-r-in-azure-sql-database.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [机器学习服务中的已知的问题](#TitleNum_1)
2. [使用 miniCRAN 创建本地包存储库](#TitleNum_2)
3. [确定 SQL 服务器上安装哪些 R 包](#TitleNum_3)
4. [在 SQL Server 上安装其他 R 包](#TitleNum_4)
5. [安装 SQL Server 机器学习 Azure 虚拟机上的功能](#TitleNum_5)
6. [安装预先训练的机器学习模型上 SQL Server](#TitleNum_6)
7. [避免在用户库中安装的 R 包上的错误](#TitleNum_7)
8. [设置用于在 Azure 上的机器学习的虚拟机](#TitleNum_8)
9. [RevoScaleR](#TitleNum_9)
10. [启用或禁用对 SQL Server 的 R 包管理](#TitleNum_10)
11. [设置 SQL Server 用于数据科学客户端](#TitleNum_11)
12. [设置 SQL Server 机器学习服务（数据库内）](#TitleNum_12)
13. [机器学习服务 （数据库） 的无人参与的安装](#TitleNum_13)
14. [步骤 3：浏览并可视化数据](#TitleNum_14)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1.&nbsp;[机器学习服务中的已知问题](known-issues-for-sql-server-machine-learning-services.md)

*更新时间： 自 2017 年 1-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 321.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00121c648c21576d5c86494137de1d4d81e2e265 c65973f6ae9253af5ecc621916ef36d7c0398789  (PR=3980  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



**Python 代码执行，或者 Python 包问题**


本部分包含特定于 SQL Server，以及与 Microsoft，发布的 Python 包相关的问题上运行 Python 的已知的问题包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

**预先训练的模型调用失败，如果对模型的路径太长**


如果在默认安装中，具体取决于你的计算机名称和实例名称安装的预先训练的模型训练的模型文件的生成完整路径可能太长，Python 读取。 将在即将发布的服务版本中解决此限制。

有几种可能的解决方法：

+ 在安装的预先训练的模型时，选择自定义位置。
+ 如果可能，请安装自定义安装路径，例如 C:\SQL\MSSQL14 下的 SQL Server 实例。MSSQLSERVER。
+ 使用 Windows 实用工具[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)创建硬链接，将模型文件映射到较短的路径。

**无法初始化 varbinary 变量中 BxlServer 导致的错误**


如果在使用 SQL Server 中运行 Python 代码`sp_execute_external_script`，并且代码具有输出类型 varbinary （max）、 varchar （max） 或类似的类型的变量，必须初始化变量，或将其设置为你的脚本的一部分。 否则，数据 exchange 组件，BxlServer，将引发错误，停止工作。

将在即将发布的服务版本中解决此限制。 解决方法是，确保将变量初始化 Python 脚本中。 可以使用任何有效的值，如以下示例所示：

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-create-a-local-package-repository-using-minicranrcreate-a-local-package-repository-using-minicranmd"></a>2.&nbsp;[创建本地包存储库使用 miniCRAN](r/create-a-local-package-repository-using-minicran.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 43.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 44b77cb127e9ffab1777216a66f0e5be9c82f3d2 65e30f10fc36acb3ce95f60f51f3501fbc98ad08  (PR=4150  ,  Filename=create-a-local-package-repository-using-minicran.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



-   **更轻松地脱机安装**： 若要将程序包安装到脱机的服务器，需要，你还可以下载所有包依赖项，使用 miniCRAN，更便于在正确的格式中获取所有依赖项。

-   **改进的版本管理**： 在多用户环境中，有很好的理由，为了避免不受限制的安装在服务器上的多个包版本。

创建之后存储库，你可以修改它通过添加新包或现有包的版本升级。

**步骤 1。安装 miniCRAN 包**


你首先创建一个 miniCRAN 存储库，以用作源。 你应在具有 internet 访问权限的计算机上创建此存储库。

1.  安装 miniCRAN 包和所需**igraph**包。

```
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
```

**步骤 2。定义包源： CRAN 镜像或 MRAN 快照**


1. 指定要在获取包中使用的镜像站点。

```
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
```

2.  指示要在其中存储收集的包的本地文件夹。 您不需要命名文件夹 miniCRAN 中;它可能是更具描述性的名称，例如"GeneticsPackages"或"ClientRPackages1.0.2"。

    只需请确保事先创建文件夹。 如果引发错误`local_repo`文件夹不存在时更高版本运行的 R 代码。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3.&nbsp;[确定 SQL 服务器上安装哪些 R 包](r/determine-which-packages-are-installed-on-sql-server.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 13d93acedc6e6b4615f1a244a2a1542910feb69e 9a065066398843a4bed318fa46d4982d712915a9  (PR=4150  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



+ 如果找到包，则返回的消息应类似"命令已成功完成。"

+ 如果无法找到或加载包，你收到如下错误:"外部脚本出错： library("RevoScaleR") 时出错： 没有调用 RevoScaleR 程序包"

**获取使用 R 的安装程序包的列表**


可通过多种方式使用 R 工具和 R 函数获取已安装或已加载的包的列表。 很多 R 开发工具都提供对象浏览器，或已安装或已在当前 R 工作区中加载的包的列表。

+ 从本地 R 实用程序，使用基础 R 函数，如`installed.packages()`中, 附带`utils`包。 若要获取的实例的准确列表，您必须显式指定的库路径或使用与实例库关联的 R 工具。

+ 若要检查特定的计算上下文中的包，可以使用 RevoScaleR 包中的下列函数。 这些函数可帮助您识别在指定的计算上下文中的包：

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

例如，运行下面的 R 代码，以获取指定的 SQL Server 计算上下文中提供的程序包的列表。

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
**另请参阅**




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-install-additional-r-packages-on-sql-serverrinstall-additional-r-packages-on-sql-servermd"></a>4.&nbsp;[在 SQL Server 上安装其他 R 包](r/install-additional-r-packages-on-sql-server.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 266.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ba48f1838857d90d6692aafc48f393777ac602fa 37de2586a344a99969bcd9a20723c021db2604a4  (PR=4150  ,  Filename=install-additional-r-packages-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



本部分提供各种的提示和与 SQL Server 上的 R 包安装相关的示例代码。

**<a name="packageVersion"></a>获取正确的包版本和格式**


可以从多个来源获取 R 包，最广为人知的是 CRAN 和 Bioconductor。 R 语言的官方站点 (<https://www.r-project.org/>) 列出了许多这样的资源。 很多包发布到 GitHub，从何处可以获取源代码。 但是，您可能提供了通过你的公司中的某个人开发的 R 包。

而不考虑源，必须确保你想要安装的程序包具有适用于 Windows 平台的二进制格式。 否则，无法在 SQL Server 环境中运行下载的包。

在下载之前，你还应检查包是否与在 SQL Server 中运行的 R 版本兼容。

**<a name="bkmk_zipPreparation"></a>下载包为压缩文件**


在没有 internet 访问权限的服务器上的安装，下载脱机安装的压缩文件的格式中的包的副本。 请不要解压缩包。

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) bioconductor，假定计算机具有 internet 访问权限的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，并选择**目标另存为**。

3.  导航到本地文件夹，zip 的包存储中，然后单击**保存**。

此过程将创建包的本地副本。 然后可以安装包，也可将压缩的包复制到的服务器，不能访问 internet。

有关的 zip 文件格式，以及如何创建 R 包内容的详细信息，我们建议本教程中，你可以从 R 项目站点的 PDF 格式下载该：[创建 R 包](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)。



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-installing-sql-server-machine-learning-features-on-an-azure-virtual-machinerinstalling-sql-server-r-services-on-an-azure-virtual-machinemd"></a>5.&nbsp;[安装 SQL Server 机器学习 Azure 虚拟机上的功能](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f4d287044b8bfda2dbe77fbf65b0d9cdd8f2ff42 2a8e33de6383f5d3af52256c5dfcb60184659eb8  (PR=4150  ,  Filename=installing-sql-server-r-services-on-an-azure-virtual-machine.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



6. 如果你计划从远程数据科学客户端连接到的实例，完成 [其他步骤-#additional-步骤） 如有必要。

**禁用 SQL Server 虚拟机上的机器学习功能**


你还可以启用或禁用现有的 SQL Server 虚拟机上的功能在任何时间。

1. 打开虚拟机边栏选项卡。
2. 单击“设置”，然后选择“SQL Server 配置”。
3. 对功能进行更改并应用。

**<a name="existing"></a>将 R Services 添加到现有的 SQL Server 2016 Enterprise VM**


如果你创建 Azure 虚拟机而无需机器学习中包含 SQL Server，你可以通过执行以下步骤添加该功能：

1. 重新运行..！包括 NotShown-ssNoVersion.../../includes/ssnoversion-md.md)] 安装程序并将功能添加上**服务器配置**向导页。
2. 启用外部脚本执行，并重新启动...！包括 NotShown-ssNoVersion.../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [设置了 SQL Server R 服务.../../ advanced-analytics/r/set-up-sql-server-r-services-in-database.md）。
3. （可选）如果需要，请为远程脚本执行配置 R 辅助角色帐户的数据库访问。
   有关详细信息，请参阅 [设置了 SQL Server R 服务.../../ advanced-analytics/r/set-up-sql-server-r-services-in-database.md）。
3. （可选）如果想要允许从远程数据科学客户端执行 R 脚本，请修改 Azure 虚拟机上的防火墙规则。 有关详细信息，请参阅 [解除阻止防火墙-#firewall）。
4. 安装或启用所需的网络库。 有关详细信息，请参阅 [添加网络协议-#network）。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-install-pretrained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>6.&nbsp;[安装预先训练的 SQL Server 上的机器学习模型](r/install-pretrained-models-sql-server.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 96.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07b51584a90568cccceea382c44155e40e09c967 db083f8536fbb2ea5886fed787872867b5de5750  (PR=4150  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    For example, to enable use of the latest version of the pretrained models for Python, in a default instance of SQL Server 2017, you would run this statement:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    On a named instance, the command would be something like this:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + 若要使用 Python 预先训练模型使用机器学习 Server （独立）：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    例如，假设使用 SQL Server 2017 安装程序的默认安装的计算机学习 Server （独立），运行此语句：

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. 版本参数支持以下值：



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-avoiding-errors-on-r-packages-installed-in-user-librariesrpackages-installed-in-user-librariesmd"></a>7.&nbsp;[避免 R 包安装在用户库上的错误](r/packages-installed-in-user-libraries.md)

*更新时间： 自 2017 年 1-10-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 52cb9a53d7d9c31ee9bc6977464ebd2a18081ff3 3537aa6755c66f12c19bb3448dc9b5c8abb9cc28  (PR=3619  ,  Filename=packages-installed-in-user-libraries.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=aecf422ca2289b2a417147eb402921bb8530d969) -->



但是，这可以永远不会处理在 SQL Server 中运行 R 解决方案时因为 R 包必须安装到与实例关联的特定的默认库。

如果包未安装到默认库中，则在尝试调用该包时，可能会收到以下错误：

*Library(xxx) 时出错： 没有名为包-name 的包*

还有一种错误开发做法将所需的 R 包安装到自定义用户的库，因为它将导致错误，如果由不到库位置具有访问另一个用户运行解决方案。

**如何将 R 包安装到访问的库**


**有关 SQL Server 2016**

使用与实例关联的包库。 有关详细信息，请参阅 [使用 SQL Server--installing-and-managing-r-packages.md 安装 R 包）

**SQL server 自 2017 年 1**

SQL Server 提供功能，可帮助你管理多个包版本，并对其授予用户权限单个包，而无需用户具有文件系统访问权限。

有关如何设置共享的包库并将用户分配到角色的详细信息，请参阅 [R 包管理 SQL Server--r-package-management-for-sql-server-r-services.md）。




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-provision-a-virtual-machine-for-machine-learning-on-azurerprovision-the-r-server-only-sql-server-2016-enterprise-vm-on-azuremd"></a>8.&nbsp;[设置用于在 Azure 上的机器学习的虚拟机](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

*更新时间： 自 2017 年 1-10-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 132.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 16439b4a8f5f4218edfcd746ed20ccbc8263dabc 1b3a8a7d1ceceaa459b3fd5640da26859df8d80b  (PR=3748  ,  Filename=provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=262e3cf5df2448bb6b532c0549c3d72daefe5a96) -->



|名称| 注释|
|----|----|----|
| **SQL Server 2016**| ***  |
|在 Windows 上的 SQL Server 2016 SP1 Enterprise|集成的高级分析的 R Services。|
|Windows Server 上的 BYOL SQL Server 2016 SP1 Enterprise |集成的高级分析的 R Services。 |
|Windows Server 2016 上的可用许可证： SQL Server 2016 SP1 开发人员 |集成的高级分析的 R Services。 |
| 数据科学虚拟机的 Windows 2012|包含用于数据科学，。 包括 Microsoft R Server Developer Edition、 SQL Server 2016 开发人员版、 Anaconda Python 分发，Julia 专业开发人员版和 Jupyter 笔记本的常用工具|
| 数据科学虚拟机-Windows 2016|包含 SQL Server 2016 Developer Edition，具有对数据库中 R 分析的支持。|
|**SQL Server 2017**| ***   |
|SQL Server 自 2017 年企业 Windows Server 2016| 具有 Python 和 R 语言支持的机器学习服务。|
|BYOL SQL Server 自 2017 年企业 Windows Server 2016|具有 Python 和 R 语言支持的机器学习服务。|
| Windows Server 上可用的 SQL Server 许可证： SQL Server 自 2017 年 Developer|具有 Python 和 R 语言支持的机器学习服务。|
| **其他**| *** |
| 机器学习服务器唯一的 SQL Server 自 2017 年 Enterprise|类似于 SQL Server 2016 Enterprise 映像，但包含的机器学习服务器的独立版本，但核心 ScaleR 和操作化功能优化适用于 Windows 环境。|
| 适用于 Windows 的机器学习服务器|机器学习服务器的独立版本包含针对 Windows 环境而优化的操作化功能。|



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-revoscalerrrevoscaler-overviewmd"></a>9.&nbsp;[RevoScaleR](r/revoscaler-overview.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_8) | [下一步](#TitleNum_10))

<!-- Source markdown line 18.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92f2dfa2e75037a932415881c55d2fd37fc6847a c6e9f17f2df82447b18beff41769ae3ebfbed562  (PR=4150  ,  Filename=revoscaler-overview.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->




RevoScaleR 是由 Microsoft，支持在规模较大的数据科学提供的机器学习函数的包。

+ 函数支持数据导入、 数据转换、 汇总、 可视化和分析。

+ _大规模_意味着操作可以针对大型数据集，以并行执行并在分布式文件系统。 算法可以在不适合在内存中，通过使用分块，以及通过组装结果完成操作后的数据集上进行操作。

+ RevoScaleR 基础上开放源代码 R 函数提供了许多改进。 没有对应于许多最常用的基础 R 函数的 RevoScaleR 函数。 RevoScaleR 函数表示为**rx**或**Rx**前缀以使它们以便于识别。

+ RevoScaleR 用作的分布式的数据科学的平台。 例如，你可以使用 RevoScaleR 计算上下文和转换与最先进的算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 你还可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)能够并行运行基础 R 函数。

RevoScaleR 操作中的示例，请参阅下列博客：

+ [生成和部署使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [每秒含机器学习服务器一百万个预测](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [预测 taxi 提示使用 MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [使用 rxExec 优化性能](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

**如何获取 RevoScaleR**




&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-enable-or-disable-r-package-management-for-sql-serverrr-package-how-to-enable-or-disablemd"></a>10.&nbsp;[启用或禁用对 SQL Server 的 R 包管理](r/r-package-how-to-enable-or-disable.md)

*更新时间： 自 2017 年 1-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_9) | [下一步](#TitleNum_11))

<!-- Source markdown line 60.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f846cd7d601459a95e694ada41e9fc5285f3de9 83a4a84adf47670c7fd4599f889f27ec3c219708  (PR=4150  ,  Filename=r-package-how-to-enable-or-disable.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    If you do not specify a user, the current security context is used.

3. 必须为安装包的每个数据库重复执行该命令。

4.  要验证是否已成功创建新的角色，请在 SQL Server Management Studio，请单击数据库，展开**安全**，然后展开**数据库角色**。

    此外可以在如下所示的 sys.database_principals 上运行查询：

```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,
        pr.authentication_type_desc, pe.state_desc,
        pe.permission_name, s.name + '.' + o.name AS ObjectName
    FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    JOIN sys.objects AS o
        ON pe.major_id = o.object_id
    JOIN sys.schemas AS s
        ON o.schema_id = s.schema_id;
```

4.  启用该功能后，可以使用具有适当权限的任何用户[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)T-SQL 添加包中的语句。 有关此工作原理的示例，请参阅[在 SQL Server 上安装其他软件包](r/install-additional-r-packages-on-sql-server.md)。

**<a name="bkmk_disable"></a>禁用包管理**




&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-set-up-a-data-science-client-for-use-with-sql-serverrset-up-a-data-science-clientmd"></a>11.&nbsp;[设置与 SQL Server 一起使用的数据科学客户端](r/set-up-a-data-science-client.md)

*更新时间： 自 2017 年 1-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_10) | [下一步](#TitleNum_12))

<!-- Source markdown line 52.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f674f5d329211e4c7d8dc464bd70f1cdef633350 8c65fc96c04f32d1e4777870774a11f9fd2ee219  (PR=3765  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



    For setup information, see [How to install R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

    To configure RTVS to use your Microsoft R client libraries, see [About Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    即使是免费的社区版包括数据科学工作负荷，安装适用于 R、 Python 和 F # 的项目模板。

    下载 Visual Studio 中，从[此站点](https://www.visualstudio.com/vs/)。

+ RStudio

    如果你偏好使用 RStudio，需要执行一些附加的步骤来使用 RevoScaleR 库：

    - 安装 Microsoft R 客户端，以获得所需的包和库。
    - 更新你的 R 路径以使用 Microsoft R 运行时。

    有关详细信息，请参阅[R 客户端-配置您的 IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide)。

**配置 IDE**


+ 用于 Visual Studio 的 R 工具

    请参阅[此站点](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)有关如何生成和调试 R 的一些示例项目使用 R Tools for Visual Studio。

+ Visual Studio 2017

    如果你安装 Microsoft R 客户端或 R Server**之前**安装 Visual Studio、 R Server 库自动检测和用于你的库路径。 如果你不安装 RevoScaleR 库中，从**R 工具**菜单上，选择**安装 R 客户端**。

**在 SQL Server 中运行 R**


此示例使用 Visual Studio 2017 Community Edition，其安装数据科学工作负荷。

1. 从**文件**菜单上，选择**新建**，然后选择**项目**。

2. -手工窗格包含预安装的模板的列表。 单击**R**，然后选择**的 R 项目**。 在**名称**框中，键入`dbtest`单击**确定**。



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>12.&nbsp;[设置 SQL Server 计算机学习 Services （数据库）](r/set-up-sql-server-r-services-in-database.md)

*更新时间： 自 2017 年 1-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_11) | [下一步](#TitleNum_13))

<!-- Source markdown line 111.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4d355f6494b417dd90dce3943e7176eaece7336e 20bddb8ffd4cf3774b812a7376c70b95ccc57e92  (PR=3980  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



   + 数据库引擎服务
   + R Services（数据库内）

7. 安装完成后，重新启动计算机。


**<a name="bkmk2017top"></a>安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）**


> [!div class="checklist"]
> * 安装数据库引擎和机器学习功能
> * 所需安装后步骤： 启用机器学习中，并重新启动
> * 可选的安装后步骤： 添加防火墙规则、 添加用户、 更改或配置服务帐户设置远程数据科学客户端。

**要开始**

1. 运行..！包括 NotShown-ssNoVersion.../../includes/ssnoversion-md.md)] 安装程序。

2. 上**安装**选项卡上，选择**新的 SQL Server 独立安装或向现有安装添加功能**。

     ![安装机器学习服务 (In-Database)--media/2017setup-installation-page-mlsvcs.png"启动带机器学习服务的数据库引擎的安装")

3. 上**功能选择**页上，选择以下选项：

    + 选择**数据库引擎服务**。 数据库引擎使用机器学习每个实例中需要。

    + 选择**机器学习服务 （数据库）**。 此选项将安装。 数据库中使用的支持选择此选项后，你可以选择机器学习语言。 你可以选择仅 R，或者你可以添加 R 和 Python。

    ![Selection--media/2017setup-features-page-mls-rpy.png 的机器学习服务功能"选择这些功能服务数据库中")

    如果不选择 R 或 Python 语言选项，安装向导正在安装仅扩展性框架，其中包括 SQL Server 受信任的快速启动板并不安装任何特定于语言的组件。  通常，我们建议你开始安装至少一种语言。 但是，如果你想要立即使用绑定过程来升级机器学习组件可能使用此选项。 有关详细信息，请参阅 [使用 SqlBindR 升级的 R Services--use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md 实例)。



&nbsp;

&nbsp;

---

<a name="TitleNum_13"/>

### <a name="13-nbsp-unattended-installation-of-machine-learning-services-in-databaserunattended-installs-of-sql-server-r-servicesmd"></a>13.&nbsp;[的机器学习服务 （数据库） 的无人参与的安装](r/unattended-installs-of-sql-server-r-services.md)

*更新时间： 自 2017 年 1-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_12) | [下一步](#TitleNum_14))

<!-- Source markdown line 75.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ad203c90adff3f515b5f16472fad9753be7a421d 6925a9276bcd4a80babc7504de50400f1a5a2940  (PR=3765  ,  Filename=unattended-installs-of-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



下面的示例演示使用添加 Python 语言安装的 SQL Server 自 2017 年机 Services （数据库） 的所需执行无提示，无人参与的参数。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

请注意所需的 SQL Server 自 2017 年中的 Python 的标志：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

**命名实例上安装 R 和 Python**


下面的示例演示执行无提示，无人参与所需的自变量安装的 SQL Server 自 2017 年机 Services （数据库） 的命名实例上。 添加 R 和 Python 的语言。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

**<a name="OldInstall"></a>SQL Server 2016 命令行安装**


下面的示例演示使用添加 R 语言安装的 SQL Server 2016 的所需执行无提示，无人参与的参数。



&nbsp;

&nbsp;

---

<a name="TitleNum_14"/>

### <a name="14-nbsp-step-3-explore-and-visualize-the-datatutorialssqldev-py3-explore-and-visualize-the-datamd"></a>14.&nbsp;[步骤 3： 浏览和可视化数据](tutorials/sqldev-py3-explore-and-visualize-the-data.md)

更新日期：2017-11-30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_13)）

<!-- Source markdown line 66.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 47edcfbd8da7cf1ea1ad03a05f86d3cd26014827 674a7c7d0e8290fc91970ed2aeda3b97d5165d75  (PR=4150  ,  Filename=sqldev-py3-explore-and-visualize-the-data.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    Class 4: `tip_amount` > $20

**创建在 T-SQL 中使用 Python 的图形**


开发数据科学解决方案通常包括深入的数据探索和数据可视化。 由于可视化效果是此类的强大工具了解数据和离群值的分布，Python 提供很多包可视化数据。 **Matplotlib**模块是其中一个可视化效果，更受欢迎的库，包括用于创建直方图、 散点图、 框图形和其他数据浏览关系图的许多函数。

在本部分中，你将了解如何使用图形使用存储的过程。 而是不是打开服务器上的映像，你存储的 Python 对象`plot`作为**varbinary**数据，然后写入该到文件，可以是共享或其他位置查看。

**创建作为 varbinary 数据绘图**


**Revoscalepy** SQL Server 自 2017 年 1 机器学习服务中包含的模块支持的功能类似于**RevoScaleR**打包成。 此示例使用的 Python 等效项`rxHistogram`进行绘图时基于数据的直方图..！包括 NotShown-tsql.../../includes/tsql-md.md)] 查询。

存储的过程返回的序列化的 Python`figure`对象的流作为**varbinary**数据。 不能直接查看二进制数据但你可以使用客户端上的 Python 代码来反序列化和查看的数字，然后将图像文件在客户端计算机上。

1. 创建存储的过程_SerializePlots_，如果 PowerShell 脚本未已执行此操作。

    - 变量`@query`定义查询文本`SELECT tipped FROM nyctaxi_sample`，这到 Python 代码块作为参数传递给脚本输入变量， `@input_data_1`。
    - Python 脚本是相当简单： **matplotlib** `figure`对象可用于进行使直方图和散点图，这些对象然后使用序列化`pickle`库。







## <a name="similar-articles"></a>类似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域它们具有新的或最近已更新的文章

- [新文章和更新的文章 (3+14)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (1 + 0): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (87+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (5+4)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (2+2)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (10+9)：Linux 版 SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (2+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (4+2)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (21+0)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章 (5+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1): **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (1+0)：SQL Server 迁移助手 (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 1): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>主题区域的任何新的或最近已更新的文章

- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX 数据对象 (ADO) sql**文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)


