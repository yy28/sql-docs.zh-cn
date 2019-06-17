---
title: 安装 R Server 或 Machine Learning Server （独立版） 使用 SQL Server 安装程序-SQL Server 机器学习
description: 设置使用 RevoScaleR 和 revoscalepy、 MicrosoftML 和其他包的 R 和 Python 开发不识别实例的独立机器学习服务器。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 911086beaaaeb28a036a764e066402d7ba6f1da7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62747069"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>安装 Machine Learning Server （独立版） 或使用 SQL Server 安装的 R Server （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安装程序包含一个“共享功能”  选项，用于安装在 SQL Server 外部运行且不支持实例的独立机器学习服务器。 在 SQL Server 2016 中，此功能称为“R Server（独立版）”  。 在 SQL Server 2017 中，它称为“Machine Learning Server（独立版）”  ，包括 R 和 Python。 

SQL Server 安装程序安装的独立服务器在功能上等同于非 SQL 品牌版本的 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支持相同的用例和方案，包括：

+ 远程执行，在同一控制台中切换本地和远程会话
+ Web 节点和计算节点的操作
+ Web 服务部署：将 R 和 Python 脚本打包到 Web 服务中的能力
+ R 和 Python 函数库的完整集合

R 和 Python 环境是与 SQL Server 分离的独立服务器，可使用独立服务器（而非 SQL Server）中提供的基础操作系统和工具对其进行配置、保护和访问。

独立服务器是 SQL Server 的附加补充，如果需要开发可以将远程计算上下文用于所有支持的数据平台的高性能机器学习解决方案，则独立服务器非常有用。 可以将执行从本地服务器转移到Spark群集或另一个 SQL Server 实例上的远程计算机服务器。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>预安装清单

如果安装了以前的版本，如 SQL Server 2016 R Server（独立版）或 Microsoft R Server，卸载现有的安装才能继续。

通常，我们建议你将独立服务器和数据库引擎实例识别安装视为互斥安装以避免资源争用，但如果你有足够的资源，则不禁止在同一台物理计算机上进行这两种安装。

只能在计算机上安装一台独立服务器：SQL Server 2017 Machine Learning Server 或  SQL Server 2016 R Server（独立版）。 请务必卸载然后再添加一个新的一个版本。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>安装修补程序要求 

对于 SQL Server 2016 仅：Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  
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

4. 上**功能选择**页上，以下选项，应已选择：

    - Microsoft Machine Learning Server （独立版）

    - 默认情况下，R 和 Python 均已选定。 你可以取消选择任一语言，但我们建议你至少安装一种支持的语言。

     ![选择 R 或 Python 功能](media/2017setup-features-page-mlsvr-rpy.png "启动 Machine Learning Server 独立安装")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 如果计算机已安装用于 SQL Server 数据库内分析的计算机学习服务，请避免安装“共享功能  。 这会创建重复的库。
    > 
    > 此外，尽管在 SQL Server 中运行的 R 或 Python 脚本由 SQL Server 管理，以免与其他数据库引擎服务使用的内存冲突，但是独立机器学习服务器没有此类限制，并且可介入其他数据库操作。 最后，数据库管理员通常会阻止通过 RDP 会话进行的远程访问，RDP 会话通常用于操作化。
    > 
    > 出于这些原因，我们通常建议你在独立于 SQL Server 机器学习服务的计算机上安装 Machine Learning Server（独立版）。

5.  接受下载和安装基本语言发行版的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步”  。 

     ![Python 许可协议](media/2017setup-python-license.png "Python 许可协议")

6.  在“准备安装”  页上，验证选择，并单击“安装”  。

完成安装后，请参阅[自定义 SQL Server R Services 的报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)出现任何错误或警告的帮助，请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动安装向导。

2. 在“安装”  选项卡上，单击“新的 R Server（独立版）安装”  。
    
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

5.  接受下载和安装基本语言发行版的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步”  。 

6.  在“准备安装”  页上，验证选择，并单击“安装”  。

完成安装后，请参阅[自定义 SQL Server R Services 的报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)出现任何错误或警告的帮助，请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

## <a name="set-environment-variables"></a>设置环境变量

对于仅 R 功能集成，应设置**MKL_CBWR**环境变量[确保一致的输出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)从 Intel Math Kernel Library (MKL) 的计算。

1. 在控制面板中，单击**系统和安全** > **系统** > **高级系统设置** >  **环境变量**。

2. 创建一个新的用户或系统变量。 

  + 到组变量名称 `MKL_CBWR`
  + 将变量的值设置为 `AUTO`

3. 重新启动服务器。

<a name="install-path"></a>

### <a name="default-installation-folders"></a>默认安装文件夹

对于 R 和 Python 开发，同一台计算机上装有多个版本是很常见的。 由 SQL Server 安装程序安装时，基础发行版安装在与用于安装的 SQL Server 版本相关联的文件夹中。

下表列出了由 Microsoft 安装程序创建的 R 和 Python 发行版的路径。 出于完整性的考虑，该表包括 SQL Server 安装程序生成的路径以及 Microsoft Machine Learning Server 的独立安装程序。

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

在连接 internet 的设备上可以下载自解压缩可执行文件。 自动应用于数据库引擎更新拉入现有的 R 和 Python 功能的累积更新。 

在连接已断开的服务器上，需执行额外的步骤。 必须获取数据库引擎的累积更新以及机器学习功能的 CAB 文件。 必须为所有文件传输到独立服务器，手动应用。

1. 使用基线实例启动。 只能应用于现有的安装累积更新：

  + 从 SQL Server 2017 初始版本的机器学习服务器 （独立版）
  + 从 SQL Server 2016 初始版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2 的 R Server （独立版）

2. 关闭任何打开的 R 或 Python 会话并停止任何进程仍在系统上运行。

3. 如果您启用了操作化，以运行 web 节点和计算节点进行 web 服务部署，备份**AppSettings.json**文件作为一项预防措施。 正在应用 SQL Server 2017 CU13 或更高版本 revises 此文件，因此你可能想要保留的原始版本的备份副本。

4. Internet 连接在设备上，单击你的 SQL Server 版本的累积更新链接。

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 下载最新的累积更新。 它是一个可执行文件。

6. 在连接 internet 的设备上，双击.exe 以运行安装程序并逐行执行向导以接受许可条款，查看受影响的功能，并监视进度，直至完成为止。

7. 在未连接到 internet 的服务器：

   + 对 R 和 Python 中获取相应的 CAB 文件。 有关下载链接，请参阅[实例上 SQL Server 数据库内分析的累积更新的下载 CAB](sql-ml-cab-downloads.md)。

   + 传输的所有文件、 主可执行文件和 CAB 文件，到脱机计算机上的文件夹。

   + 双击以运行安装程序的.exe。 时未连接到 internet 的服务器上安装的累计更新，系统会提示选择 R 和 Python 的.cab 文件的位置。

8. 安装后，已启用包含 web 节点和计算节点的操作化的服务器上编辑**AppSettings.json**，添加一个"MMLResourcePath"项，直接位于"MMLNativePath"下面：

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [运行管理 CLI 实用程序](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)重新启动 web 和计算节点。 有关步骤和语法，请参阅[监视器、 启动和停止 web 和计算节点](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)。

## <a name="development-tools"></a>开发工具

开发 IDE 未安装的一部分安装。 有关配置开发环境的详细信息，请参阅[设置的 R 工具](../r/set-up-a-data-science-client.md)并[设置 Python 工具](../python/setup-python-client-tools-sql.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程：R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程：在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [教程：面向 Python 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

若要查看基于实际场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
