---
title: "安装机器学习 Components without Internet Access |Microsoft 文档"
ms.custom: 
ms.date: 04/20/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7307104b9ad5df2bb8f034525cc82847d21a14bf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>安装机器学习 Components without Internet Access

由于 SQL Server 2016 或 SQL Server 2017 所提供的 R 和 Python 组件是开放源代码，则 Microsoft 不默认情况下安装 R 或 Python 的组件。

相反，我们提供相关安装程序，为方便起见在 Microsoft 下载中心和其他受信任的站点上捆绑包。 必须同意适当的许可，，然后，SQL Server 安装程序将为你安装 R 或 Python 的组件。

本主题提供的下载位置中的安装程序和脱机安装程序过程的概述。

## <a name="installation-process"></a>安装过程

通常情况下，使用 SQL Server 2016 和 SQL Server 自 2017 年中的计算机组件的安装程序需要 Internet 连接。 SQL Server 安装程序运行时，如果选择了任何机 learnig 选项，安装程序将检查 Python 或 R 安装程序，作为以及任何其他必需的组件。 如果没有 Internet 连接，SQL Server 将为你来安装它们。

> [!IMPORTANT]
> 在没有 Internet 访问服务器上，你必须在继续执行安装程序之前下载其他安装程序。

在最低限度上，你将需要下载的 R 或 Python 的安装程序支持的版本或要安装的 SQL Server 的内部版本号。

根据你的服务器的配置，你可能需要其他组件，如.NET 核心。  请参阅[其他组件](#bkmk_OtherComponents)有关详细信息。

下载安装程序后，你使用它们时安装的 SQL Server 安装程序一部分的功能。

### <a name="step-1-obtain-additional-installers"></a>步骤 1. 获取其他安装程序

有关**R**在 SQL Server 2016 和 SQL Server 自 2017 年中，你将需要获取两个不同的安装程序。 使用 SQL Server 安装向导可以确保按正确的顺序安装它们。

+ 安装程序与**SRO**名称中提供的开放源组件。
+ 与 Insallers **SRS**名称中包含提供由 Microsoft，包括数据库的集成组件。


有关**Python**在 SQL Server 自 2017 年，下载单个的 CAB 文件中和任何必备组件。


1. 从 [Microsoft 下载中心站点](#installerlocs)将安装程序下载到可以访问 Internet 的计算机，此时请选择保存安装程序，而不要运行它。
2. 安装程序 (CAB) 文件复制到将在其中安装机学习组件的计算机。
3. 目前，安装向导默认情况下安装英语。 若要安装使用另一种语言，先修改安装程序文件名称，如下所述：[为不同的语言区域设置所需的修改](#modslocales)。
4. 下载是必需的如 MPI 或.NET Core 的任何其他组件。
5. （可选） 可以下载存档的源代码的开放源组件，但这不是 SQL Server 安装程序需要，可以在任何时候完成。 有关详细信息，请参阅[R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。


> [!NOTE]
> 请务必获取与所要安装的 SQL Server 版本匹配的文件。
> 
> SQL Server 自 2017 年 1 CTP 2.0 中提供了 Python 的支持。 早期版本中，包括 SQL Server 2016，不支持 Python。

对于 SQL Server 2016 中的 R 服务的脱机安装过程的分步演练，我们建议通过文章[SQL Server 客户咨询团队](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。 此文还介绍了修补和补充安装方案。


### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>步骤 2. 运行脱机安装程序使用 SQL Server 安装向导

1. 运行 SQL Server 安装向导。
2. 当安装向导显示授权页上时，单击**接受**。
3. 对话框随即打开，提示您输入**安装路径**的所需的包。
4. 单击**浏览**以查找包含你前面记的安装程序文件的文件夹。
5. 如果找到了正确的文件，可以单击“下一步”指示相应的组件可用。
10. 完成 SQL Server 安装向导。
11. 执行所需的安装后步骤，若要确保启用该服务。

## <a name="installerlocs"></a>下载

发行版本  |下载链接  
---------|---------
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
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 GDR**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 自 2017 年 1 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 自 2017 年 1 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 自 2017 年 1 CTP 1.4** |
Microsoft R Open     |[SRO_xxxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_xxx.xxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 自 2017 年 1 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Microsoft Python 打开     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python 服务器    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)

如果你想要查看 Microsoft R 的源代码，它是可供下载的存档文件采用.tar 格式：[下载 R Server 安装程序](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download)

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

在连接了 Internet 的计算机上，如果在安装 SQL Server 的过程中下载了 cab 文件，安装向导会检测本地语言并自动更改安装程序的语言。

但是，如果在未连接 Internet 的计算机上安装某个本地化版本的 SQL Server，并且将 R 安装程序下载到本地共享，则必须手动编辑所下载文件的名称，并为正在安装的语言插入正确的语言标识符。

例如，如果安装日语版 SQL Server，应将文件名称从 SRS_8.0.3.0_**1033**.cab 更改为 SRS_8.0.3.0_**1041**.cab。


## <a name="slipstream-upgrades"></a>版本补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点在于，可以在执行安装的同时更新 SQL Server，避免以后单独重新启动。

+ 如果服务器无法访问 Internet，则在开始执行更新过程**之前**，必须下载 SQL Server 安装程序，然后下载 R 组件安装程序的匹配版本。  默认情况下，与 SQL Server 不包括 R 组件。

+ 如果你是*添加*到这些组件*现有*安装，使用更新的版本的 SQL Server 安装程序中，并相应更新的其他组件的版本。 当你指定的 R 功能是要安装时，安装程序将查找匹配的版本为机器学习组件的安装程序。

## <a name="command-line-arguments-for-setup"></a>安装程序命令行参数

在执行无人参与的安装时，你将需要提供以下命令行自变量。 请注意，不需要设置任何其他标志，若要安装其他所需的组件。 默认情况下以无提示方式安装系统必备组件，如.NET 核心。

**安装程序的位置**

- `/UPDATESOURCE`若要指定包含 SQL Server 更新安装程序的本地文件的位置
- `/MRCACHEDIRECTORY`若要指定包含的 R 组件 CAB 文件的文件夹

**SQL Server 2016 中的 R 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/IACCEPTROPENLICENSETERMS="True"`若要接受许可协议的单独 R

**SQL Server SQL Server 自 2017 年中的 R 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/SQL_INST_MR`若要使用 R
- `/IACCEPTROPENLICENSETERMS="True"`若要接受许可协议的单独 R

**SQL Server 自 2017 年中的 Python 组件**

- `/ADVANCEDANALYTICS`若要获得有关外部脚本引擎支持
- `/SQL_INST_MPY`若要使用 Python
- `/IACCEPTPYTHONLICENSETERMS="True"`若要接受许可协议的单独 R

> [!TIP]
> 由 R 服务支持团队这篇文章演示如何在 SQL Server 2016 中执行的无人参与的安装或升级 R services:[在没有 Internet 访问权限的计算机上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

## <a name="see-also"></a>另请参阅

[安装 Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)


