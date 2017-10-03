---
title: "安装没有 internet 访问权限的机器学习组件 |Microsoft 文档"
ms.custom: 
ms.date: 09/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 41ff26c5ff2c41f600be5f45fd66dec31672b803
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>安装没有 internet 访问权限的机器学习组件

由于提供与 SQL Server 2016 和 SQL Server 2017 R 和 Python 组件是开放源代码，Microsoft 不默认情况下安装 R 或 Python 的组件。

相反，我们提供相关安装程序，为方便起见在 Microsoft 下载中心和其他受信任的站点上捆绑包。 你必须同意适当的许可，和 SQL Server 安装程序将为你安装 R 或 Python 的组件。

本主题提供的下载位置中的安装程序和脱机安装程序过程的概述。

## <a name="installation-process"></a>安装过程

通常情况下，使用 SQL Server 2016 和 SQL Server 自 2017 年中的计算机组件的安装程序需要 internet 连接。 SQL Server 安装程序运行时，如果选择了任何机器学习选项，安装程序正在检查 Python 或 R 安装程序，作为以及任何其他必需的组件。

+ **如果计算机具有 internet 连接**

    SQL Server 查找并下载的组件，然后将其安装在安装过程。 你必须接受单独安装每个开放源组件 （R 或 Python） 的许可条款。

+ **如果计算机没有 internet 访问权限**

    在继续执行安装程序之前，必须下载其他安装程序。 在最低限度上，下载的要安装的 SQL Server 版本支持的 R 或 Python 安装程序。

    根据你的服务器的配置，你可能需要其他组件。  请参阅[其他组件](#bkmk_OtherComponents)有关详细信息。

    下载安装程序后，你使用它们时安装的 SQL Server 安装程序一部分的功能。

### <a name="step-1-obtain-additional-installers"></a>步骤 1. 获取其他安装程序

有关**R**在 SQL Server 2016 和 SQL Server 自 2017 年中，你将需要获取两个不同的安装程序。 SQL Server 安装向导可确保按正确的顺序安装它们。

+ 安装程序与**SRO**名称中提供的开放源组件。
+ 安装程序与**SRS**名称中包含提供由 Microsoft，包括数据库的集成组件。

有关**Python**在 SQL Server 自 2017 年，下载单个的 CAB 文件中和任何必备组件。

1. 下载的安装程序[Microsoft 下载中心站点](#installerlocs)到计算机具有 internet 访问权限，并保存安装程序，而无需运行它。
2. 安装程序 (CAB) 文件复制到你想要安装机器学习组件的计算机。
3. 在 SQL Server 2016 中，安装向导默认情况下安装英语。 安装使用不同的语言所需的修改安装程序文件的名称，如下所述：[不同的语言区域设置所需修改](#modslocales)。
    对于 SQL Server 自 2017 年，正确的语言被标识基于实例的区域设置。
4. 下载是必需的如 MPI 或.NET Core 的任何其他组件。
5. （可选） 可以下载存档的源代码的开放源组件，但这不是 SQL Server 安装程序需要，可以在任何时候完成。 有关详细信息，请参阅[R Server for Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)。

对于 SQL Server 2016 中的 R 服务的脱机安装过程的分步演练，我们建议通过文章[SQL Server 客户咨询团队](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。 本文包括屏幕快照，并且还涵盖了修补和 slipstream 安装方案。

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>步骤 2. 运行脱机安装程序使用 SQL Server 安装向导

1. 运行 SQL Server 安装向导。
2. 当安装向导显示授权页上时，单击**接受**。
3. 对话框随即打开，提示您输入**安装路径**的所需的包。
4. 单击**浏览**以查找包含你前面记的安装程序文件的文件夹。
5. 如果找到了正确的文件，可以单击“下一步”指示相应的组件可用。
10. 完成 SQL Server 安装向导。
11. 执行所需的安装后步骤，若要确保启用该服务。

## <a name="installerlocs"></a>从哪里下载机学习组件

> [!NOTE]
> 请确保获取你要安装的 SQL Server 的版本匹配的文件。
> 
> 从 SQL Server 自 2017 年 1 CTP 2.0 开始提供的 Python 的支持。 早期版本中，包括 SQL Server 2016，不支持 Python。

+ [若要获取 SQL Server 2016 的 R 组件](#bkmk_2016Installers)

+ [若要获取 SQL Server 2017 R 或 Python 的组件](#bkmk_2017Installers)

### <a name="bkmk_2017Installers"></a>下载 SQL server 自 2017 年 1

发行版本  |下载链接  |
---------|---------|
**SQL Server 自 2017 年 1 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 自 2017 年 1 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 自 2017 年 1 CTP 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 自 2017 年 1 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Microsoft Python 打开     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python 服务器    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 自 2017 年 1 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
Microsoft Python 打开     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft Python 服务器    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 自 2017 年 1 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
Microsoft Python 打开     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft Python 服务器    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|

### <a name="bkmk_2016Installers"></a>SQL Server 2016 的的下载

> [!IMPORTANT]
> 
> 在安装 SQL Server 2016 SP1 CU4 或 SP1 CU5 脱机时，下载 SRO_3.2.2.16000_1033.cab。 如果在安装程序对话框中所示，可以从 FWLINK 831785 下载 SRO_3.2.2.13000_1033.cab，重命名文件作为 SRO_3.2.2.16000_1033.cab 安装累积更新之前。

发行版本  |下载链接  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     | 无更改;使用以前 |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前 |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 SP 1 CU4 和 GDR**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server    |无更改;使用以前 |

如果你想要查看 Microsoft R 的源代码，它是可供下载的存档文件采用.tar 格式：[下载 R Server 安装程序](https://docs.microsoft.com/r-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>附加的先决条件

根据所用的环境，可能需要为以下必备组件创建安装程序的本地副本。

组件  |版本
---------|---------
[Microsoft AS OLE DB Provider for SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0


## <a name="modslocales"></a>安装适用于不同的语言区域设置

如果你下载。具有 internet 访问权限，安装向导的计算机上的 SQL Server 安装程序一部分的 CAB 文件检测本地语言，并会自动更改安装的语言。

但是，具体取决于你的 SQL Server 版本，你可能需要执行其他步骤来在没有 internet 访问的计算机上安装本地化的 R 组件。

+ **有关 SQL Server 2016**

   将 R 安装程序下载到本地共享后，你可能需要手动编辑要插入正在安装的语言的正确的语言标识符的下载文件的名称。

    例如，若要安装日语版本的 SQL Server，你将更改文件的名称从 SRS_8.0.3.0_**1033年**到 SRS_8.0.3.0_.cab**1041年**.cab。

    > [!IMPORTANT]
    > 此问题适用仅为早期版本，并在更高版本已修复。
    > 如果安装程序返回一条消息，它不能安装正确的语言，只能使用此解决方法。

+ **SQL server 自 2017 年 1**

    下载。R 或 Python 组件的 CAB 文件。
    
    检测到基于服务器的区域设置时的语言。 正确的区域设置会自动安装使用下载。CAB 文件。

## <a name="slipstream-upgrades"></a>版本补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点在于，可以在执行安装的同时更新 SQL Server，避免以后单独重新启动。

+ 如果服务器无法访问 Internet，则在开始执行更新过程**之前**，必须下载 SQL Server 安装程序，然后下载 R 组件安装程序的匹配版本。  默认情况下，与 SQL Server 不包括 R 组件。

+ 如果你是*添加*到这些组件*现有*安装，使用更新的版本的 SQL Server 安装程序中，并相应更新的其他组件的版本。 指定要安装的 R 功能时，安装程序将查找匹配的版本为机器学习组件的安装程序。

## <a name="command-line-arguments-for-setup"></a>安装程序命令行参数

在执行无人参与的安装时，必须提供以下命令行自变量。 但是，不需要设置任何其他标志，以安装其他所需的组件;默认情况下以无提示方式安装系统必备组件，如.NET 核心。

**安装程序的位置**

- `/UPDATESOURCE`若要指定包含 SQL Server 更新安装程序的本地文件的位置
- `/MRCACHEDIRECTORY`若要指定包含的 R 组件 CAB 文件的文件夹

**SQL Server 2016 中的 R 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/IACCEPTROPENLICENSETERMS="True"`若要接受许可协议的单独 R

**SQL Server 自 2017 年中的 R 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/SQL_INST_MR`若要使用 R
- `/IACCEPTROPENLICENSETERMS="True"`若要接受许可协议的单独 R

**SQL Server 自 2017 年中的 Python 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/SQL_INST_MPY`若要使用 Python
- `/IACCEPTPYTHONLICENSETERMS="True"`若要接受许可协议的单独 R


> [!NOTE]
> 通过在 SQL Server 安装程序中使用参数，不能为快速启动板中更改服务帐户。 我们建议你安装使用默认服务帐户，然后修改使用 SQL Server 配置管理器的服务帐户。 这么做，请务必重新启动快速启动板服务。

## <a name="see-also"></a>另请参阅

[安装 Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

由 R 服务支持团队这篇文章演示如何在 SQL Server 2016 中执行的无人参与的安装或升级 R services:[在没有 Internet 访问权限的计算机上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。
