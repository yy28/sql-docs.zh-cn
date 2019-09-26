---
title: 使用 SQL Server 安装程序安装 R Server 或 Machine Learning Server (独立版)
description: 使用 RevoScaleR、revoscalepy、MicrosoftML 和其他包为 R 和 Python 开发设置不能识别实例的独立机器学习服务器。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f9835bae00aab15ee902dfe77dcf211eb412bc96
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271952"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>使用 SQL Server 安装程序安装 Machine Learning Server (独立版) 或 R Server (独立版)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server 安装程序包含一个“共享功能”选项，用于安装在 SQL Server 外部运行且不支持实例的独立机器学习服务器。 它被称为**Machine Learning Server （独立）** ，包括 R 和 Python。 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server 安装程序包含一个“共享功能”选项，用于安装在 SQL Server 外部运行且不支持实例的独立机器学习服务器。 在 SQL Server 2016 中，此功能称为“R Server（独立版）”。  
::: moniker-end

SQL Server 安装程序安装的独立服务器在功能上等同于非 SQL 品牌版本的 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)，支持相同的用例和方案，包括：

+ 远程执行，在同一控制台中切换本地和远程会话
+ Web 节点和计算节点的操作
+ Web 服务部署：将 R 和 Python 脚本打包到 Web 服务中的能力
+ 完整的 R 和 Python 函数库集合

R 和 Python 环境是与 SQL Server 分离的独立服务器，可使用独立服务器（而非 SQL Server）中提供的基础操作系统和工具对其进行配置、保护和访问。

独立服务器是 SQL Server 的附加补充，如果需要开发可以将远程计算上下文用于所有支持的数据平台的高性能机器学习解决方案，则独立服务器非常有用。 可以将执行从本地服务器转移到Spark群集或另一个 SQL Server 实例上的远程计算机服务器。

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>预安装清单

如果安装了以前的版本，如 SQL Server 2016 R Server（独立版）或 Microsoft R Server，卸载现有的安装才能继续。

通常，我们建议你将独立服务器和数据库引擎实例识别安装视为互斥安装以避免资源争用，但如果你有足够的资源，则不禁止在同一台物理计算机上进行这两种安装。

计算机上只能有一台独立服务器： SQL Server Machine Learning Server （独立）或 SQL Server R Server （独立版）。 请确保在添加新版本之前卸载一个版本。

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>安装修补程序要求 

仅适用于 2016 SQL Server:Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  
::: moniker-end

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动安装向导。

2. 单击 "**安装**" 选项卡, 然后选择 "**新建 Machine Learning Server (独立) 安装**"。
    
     ![独立安装 Machine Learning Server](media/2017setup-installation-page-mlsvr.png "开始 Machine Learning Server 独立安装")

3. 完成规则检查后, 接受 SQL Server 许可条款, 并选择新的安装。

4. 在 "**功能选择**" 页上, 应已选择以下选项:

    - Microsoft Machine Learning Server (独立)

    - 默认情况下，R 和 Python 均已选定。 你可以取消选择任一语言，但我们建议你至少安装一种支持的语言。

     ![选择 R 或 Python 功能](media/2017setup-features-page-mlsvr-rpy.png "开始 Machine Learning Server 独立安装")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 如果计算机已安装用于 SQL Server 数据库内分析的计算机学习服务，请避免安装“共享功能。 这会创建重复的库。
    > 
    > 此外，尽管在 SQL Server 中运行的 R 或 Python 脚本由 SQL Server 管理，以免与其他数据库引擎服务使用的内存冲突，但是独立机器学习服务器没有此类限制，并且可介入其他数据库操作。 最后，数据库管理员通常会阻止通过 RDP 会话进行的远程访问，RDP 会话通常用于操作化。
    > 
    > 出于这些原因，我们通常建议你在独立于 SQL Server 机器学习服务的计算机上安装 Machine Learning Server（独立版）。

5.  接受下载和安装基本语言分发的许可条款。 当“接受” 按钮变为不可用时，可以单击“下一步”。 

     ![Python 许可协议](media/2017setup-python-license.png "Python 许可协议")

6.  在“准备安装” 页上，验证选择，并单击“安装”。

安装完成后, 请参阅[SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)以获取有关任何错误或警告的帮助, 请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动安装向导。

2. 在“安装”选项卡上，单击“新的 R Server（独立版）安装”。
    
     ![启动 R Server 独立版的安装](media/2016-setup-installation-rsvr.png "启动 R Server 独立版的安装")

3. 完成规则检查后, 接受 SQL Server 许可条款, 并选择新的安装。

4.  在“功能选择” 页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    ![R Server 独立版的功能选择](media/2016setup-rserver-features.png "R Server 独立版的功能选择")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 如果运行安装程序的计算机上已安装了 R Services 进行 SQL Server 数据库内分析, 则应避免安装**共享功能**。 这会创建重复的库。
    > 
    > 在 SQL Server 中运行的 R 脚本是由 SQL Server 管理的, 因此不会与其他数据库引擎服务使用的内存发生冲突, 而独立的 R 服务器没有此类约束, 并且可能会干扰其他数据库操作。
    > 
    > 我们通常建议在 SQL Server R Services (数据库内) 的不同计算机上安装 R Server (独立版)。

5.  接受下载和安装基本语言分发的许可条款。 当“接受” 按钮变为不可用时，可以单击“下一步”。 

6.  在“准备安装” 页上，验证选择，并单击“安装”。

安装完成后, 请参阅[SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)以获取有关任何错误或警告的帮助, 请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。
::: moniker-end

## <a name="set-environment-variables"></a>设置环境变量

仅适用于 R 功能集成，应设置**MKL_CBWR**环境变量，以[确保](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)从 Intel 数学内核库（MKL）计算中进行一致的输出。

1. 在控制面板中, 单击 "**系统和安全** > **系统** > " "**高级系统设置** > " "**环境变量**"。

2. 创建新的用户或系统变量。 

  + 将变量名称设置为`MKL_CBWR`
  + 将变量值设置为`AUTO`

3. 重新启动服务器。

<a name="install-path"></a>

### <a name="default-installation-folders"></a>默认安装文件夹

对于 R 和 Python 开发，同一台计算机上装有多个版本是很常见的。 由 SQL Server 安装程序安装时，基础发行版安装在与用于安装的 SQL Server 版本相关联的文件夹中。

下表列出了由 Microsoft 安装程序创建的 R 和 Python 发行版的路径。 出于完整性的考虑，该表包括 SQL Server 安装程序生成的路径以及 Microsoft Machine Learning Server 的独立安装程序。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|SQL Server 2017 Machine Learning Server (独立版) |  SQL Server 2017 安装向导 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (独立) |  Windows 独立安装程序 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 机器学习服务（数据库内） |SQL Server 2017 安装向导, with R language 选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (独立版) |  SQL Server 2016 安装向导 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (数据库内) |SQL Server 2016 安装向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>应用更新

建议将最新的累积更新应用于数据库引擎和机器学习组件。 累积更新是通过安装程序安装的。 

在连接 internet 的设备上, 你可以下载一个自解压缩的可执行文件。 为数据库引擎应用更新会自动拉取现有 R 和 Python 功能的累积更新。 

在连接已断开的服务器上，需执行额外的步骤。 必须获取数据库引擎的累积更新以及机器学习功能的 CAB 文件。 所有文件都必须传输到隔离服务器并手动应用。

1. 开始使用基线实例。 只能对现有安装应用累积更新:

  + 从 SQL Server 2017 初始版本 Machine Learning Server (独立)
  + R Server (独立版) SQL Server 2016 初始版本 SQL Server 2016 SP 1, 或 SQL Server 2016 SP 2

2. 关闭所有打开的 R 或 Python 会话, 并停止系统上仍在运行的任何进程。

3. 如果已启用操作化作为 web 节点和计算节点用于 web 服务部署, 请备份**AppSettings**文件作为预防措施。 应用 SQL Server 2017 CU13 或更高版本将修改此文件, 因此你可能需要备份副本来保留原始版本。

4. 在连接 internet 的设备上, 单击你的 SQL Server 版本的累积更新链接。

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

5. 下载最新的累积更新。 它是一个可执行文件。

6. 在连接 internet 的设备上, 双击 .exe 以运行安装程序, 并逐步完成向导以接受许可条款, 查看受影响的功能, 并监视进度直到完成。

7. 在无 internet 连接的服务器上:

   + 获取 R 和 Python 对应的 CAB 文件。 有关下载链接, 请参阅[CAB 下载以了解 SQL Server 数据库内分析实例中的累积更新](sql-ml-cab-downloads.md)。

   + 将主可执行文件和 CAB 文件的所有文件传输到脱机计算机上的文件夹。

   + 双击 .exe 以运行安装程序。 在没有 internet 连接的服务器上安装累计更新时, 系统将提示你选择 R 和 Python 的 .cab 文件的位置。

8. 安装后, 在已启用 web 节点和计算节点操作化的服务器上, 编辑**AppSettings**, 在 "MMLNativePath" 下直接添加 "MMLResourcePath" 项:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [运行管理 CLI 实用程序](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch)以重新启动 web 和计算节点。 有关步骤和语法, 请参阅[监视、启动和停止 web 和计算节点](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start)。

## <a name="development-tools"></a>开发工具

不会在安装过程中安装开发 IDE。 有关配置开发环境的详细信息, 请参阅[设置 R 工具](../r/set-up-a-data-science-client.md)和[设置 Python 工具](../python/setup-python-client-tools-sql.md)。

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 一起使用：

+ [教程：在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [教程：适用于 Python 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

若要查看基于真实场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
