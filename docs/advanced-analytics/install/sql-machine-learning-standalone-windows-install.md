---
title: 安装 R Server 或 Machine Learning Server （独立版） 使用 SQL Server 安装程序 |Microsoft Docs
description: 设置使用 RevoScaleR 和 revoscalepy、 MicrosoftML 和其他包的 R 和 Python 开发不识别实例的独立机器学习服务器。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 70fa652e876f1011bc2d74df56104671b33775b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187487"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>安装 Machine Learning Server （独立版） 或使用 SQL Server 安装的 R Server （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安装程序包含**共享的功能**选项用于安装非实例感知，在 SQL Server 外部运行的独立机器学习服务器。 在 SQL Server 2016 中，此功能称为**R Server （独立版）**。 在 SQL Server 2017 中，名为**Machine Learning Server （独立版）** 并包括 R 和 Python。 

独立服务器安装的 SQL Server 安装程序在功能上等效于非 SQL 品牌版本的[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支持同一个用例和方案，其中包括：

+ 远程执行，在同一个控制台中的本地和远程会话之间切换
+ 包含 web 节点和计算节点的操作化
+ Web 服务部署： 打包成 web 服务的 R 和 Python 脚本的功能
+ R 和 Python 函数库的完整集合

从 SQL Server 中分离的独立服务器，作为 R 和 Python 环境配置，保护安全和访问使用基础操作系统和独立服务器，非 SQL Server 中提供的工具。

SQL Server 的附加补充，作为独立的服务器是开发高性能的机器学习可以使用支持的数据平台的完整范围的远程计算上下文的解决方案所需的情况下很有用。 你可以上移执行从本地服务器到远程的机器学习服务器在 Spark 群集上或另一个 SQL Server 实例上。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>预安装清单

如果安装了以前的版本，如 SQL Server 2016 R Server （独立版） 或 Microsoft R Server，卸载现有的安装才能继续。

作为一般规则，我们建议将独立服务器和数据库引擎识别实例的安装作为相互独占以避免资源争用，但如果您有足够的资源，没有针对安装这两个不禁止在同一台物理计算机。

只能在计算机上有一台独立服务器： SQL Server 2017 机器学习服务器或 SQL Server 2016 R Server （独立版）。 您必须手动卸载然后再安装不同版本的一个版本。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>安装修补程序要求 

SQL Server 2016: Microsoft 已发现的特定版本的 SQL server 安装的必备组件的 Microsoft VC + + 2013年运行时二进制文件的问题。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  
::: moniker-end

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动安装向导。

2. 单击**安装**选项卡，然后选择**新机器学习服务器 （独立版） 安装**。
    
     ![安装 Machine Learning Server 独立版](media/2017setup-installation-page-mlsvr.png "启动 Machine Learning Server 独立安装")

3. 规则检查完成后，接受 SQL Server 许可条款，然后选择新的安装。

4. 在**功能选择**页上，以下选项，应已选择：

    - Microsoft Machine Learning Server （独立版）

    - 默认情况下，R和Python都被选中。您可以取消选择任一语言，但我们建议您至少安装一种受支持的语言。

     ![安装 Machine Learning Server 独立版](media/2017setup-features-page-mlsvr-rpy.png "启动 Machine Learning Server 独立安装")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 避免安装**共享功能**如果计算机已安装的 SQL Server 数据库内分析的机器学习服务。 这会创建重复的库。
    > 
    > 此外，而 SQL Server 中运行的 R 或 Python 脚本由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，则独立机器学习服务器将没有此类约束，并可能会干扰其他数据库操作. 最后，数据库管理员通常会阻止通过 RDP 会话中，它通常用于操作化，远程访问。
    > 
    > 出于这些原因，我们通常建议您从 SQL Server 机器学习服务的单独计算机上安装机器学习服务器 （独立版）。

5.  接受下载和安装基本语言发行版的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。 

     ![Python 许可协议](media/2017setup-python-license.png "Python 许可协议")

6.  在“准备安装”  页上，验证选择，并单击“安装” 。

完成安装后，请参阅[自定义 SQL Server R Services 的报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)出现任何错误或警告的帮助，请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动安装向导。

2. 上**安装**选项卡上，单击**新的 R Server （独立版） 安装**。
    
     ![启动的 R Server 独立版的安装程序](media/2016-setup-installation-rsvr.png "启动的 R Server 独立版的安装程序")

3. 规则检查完成后，接受 SQL Server 许可条款，然后选择新的安装。

4.  在“功能选择”  页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    ![功能选择 R Server 独立版](media/2016setup-rserver-features.png "功能选择 R Server 独立版")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 避免安装**共享功能**如果您运行安装程序的计算机上的 R Services 已安装的 SQL Server 数据库内分析。 这会创建重复的库。
    > 
    > SQL Server 中运行 R 脚本由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，而独立 R Server 没有此类约束，并可能会干扰其他数据库操作。
    > 
    > 我们通常建议安装 R Server （独立版） 的单独计算机上从 SQL Server R Services （数据库内）。

5.  接受下载和安装基本语言发行版的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。 

6.  在“准备安装”  页上，验证选择，并单击“安装” 。

完成安装后，请参阅[自定义 SQL Server R Services 的报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)出现任何错误或警告的帮助，请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

### <a name="default-installation-folders"></a>默认安装文件夹

对于 R 和 Python 开发，常见方法是在同一计算机上拥有多个版本。 安装的 SQL Server 安装程序，基础发行版安装在用于安装的 SQL Server 版本关联的文件夹中。

下表列出了由 Microsoft 安装程序创建的 R 和 Python 分发版的路径。 出于完整性的考虑，此表包括生成的 SQL Server 安装程序，以及 Microsoft Machine Learning Server 独立安装程序的路径。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|SQL Server 2017 机器学习服务器 （独立版） |  SQL Server 2017 安装程序向导 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server （独立版） |  Windows 独立安装程序 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 机器学习服务 （数据库内） |SQL Server 2017 安装程序向导中，使用 R 语言选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server （独立版） |  SQL Server 2016 安装向导 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services （数据库内） |SQL Server 2016 安装向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

我们建议将最新的累积更新应用到数据库引擎和机器学习组件。 通过安装程序安装累积更新。 

在连接 internet 的设备上通常可通过 Windows 更新应用累积更新，但还可以使用以下步骤，受控的更新。 当在应用于数据库引擎更新时，安装程序中取出独立服务器安装任何 R 或 Python 功能的累积的更新。 

断开连接的服务器上执行额外的步骤是必需的。 你必须获取针对数据库引擎的累积更新以及机器学习功能的 CAB 文件。 必须为所有文件传输到独立服务器，手动应用。

1. 使用基线实例启动。 只能应用于现有的安装累积更新：

  + 从 SQL Server 2017 初始版本的机器学习服务器 （独立版）
  + 从 SQL Server 2016 初始版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2 的 R Server （独立版）

2. 在 internet 上连接了设备，请转到你的 SQL Server 版本的累积更新列表。

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 下载最新的累积更新。 它是一个可执行文件。

4. 在连接 internet 的设备上，双击.exe 以运行安装程序并逐行执行向导以接受许可条款，查看受影响的功能，并监视进度，直至完成为止。

5. 在未连接到 internet 的服务器：

   + 对 R 和 Python 中获取相应的 CAB 文件。 有关下载链接，请参阅[实例上 SQL Server 数据库内分析的累积更新的下载 CAB](sql-ml-cab-downloads.md)。

   + 传输的所有文件、 主可执行文件和 CAB 文件，到脱机计算机上的文件夹。

   + 双击以运行安装程序的.exe。 时未连接到 internet 的服务器上安装的累计更新，系统会提示选择 R 和 Python 的.cab 文件的位置。

6. 安装后，已启用包含 web 节点和计算节点的操作化的服务器上编辑**appsettings.json**，添加一个"MMLResourcePath"项，直接位于"MMLNativePath"下面：

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

7. [运行管理 CLI 实用程序](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)重新启动 web 和计算节点。 有关步骤和语法，请参阅[监视器、 启动和停止 web 和计算节点](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)。

## <a name="development-tools"></a>开发工具

开发 IDE 未安装的一部分安装。 有关配置开发环境的详细信息，请参阅[设置的 R 工具](../r/set-up-a-data-science-client.md)并[设置 Python 工具](../python/setup-python-client-tools-sql.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
