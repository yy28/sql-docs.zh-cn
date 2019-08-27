---
title: 升级 R 和 Python 组件
description: 使用 sqlbindr 将 R 和 Python 升级到 SQL Server 机器学习服务或 SQL Server R Services, 以将其绑定到 Machine Learning Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634552"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升级 SQL Server 实例中的机器学习 (R 和 Python) 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server中的R和Python集成包括开源代码和Microsoft专有包。 在标准SQL Server服务框架下，是根据SQL Server发布周期来更新包的，同时提供针对当前版本中现有包错误的修复程序，但不存在主要版本升级。 

不过, 很多数据科学家都习惯于在可用时使用较新的包。 对于 SQL Server 机器学习服务 (数据库内) 和 SQL Server R Services (数据库内), 可以通过*绑定*到**Microsoft Machine Learning Server**来获取[较新版本的 R 和 Python](#version-map) 。 

## <a name="what-is-binding"></a>什么是绑定？

绑定是一个安装过程, 它通过[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)的新的可执行文件、库和工具交换 R_SERVICES 和 PYTHON_SERVICES 文件夹的内容。

与更新的组件一起在维护模型中提供了一个交换机。 你的服务更新现在符合[新式生命周期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)中[Microsoft R Server & Machine Learning Server 的支持时间线](https://docs.microsoft.com/machine-learning-server/resources-servicing-support), 而不是[SQL Server 产品生命周期](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)的[SQL Server 累积更新](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)。

除了组件版本和服务更新, 绑定不会更改你的安装基础:R 和 Python 集成仍是数据库引擎实例的一部分, 授权不会改变 (与绑定无关的额外成本), SQL Server 支持策略仍可用于数据库引擎。 本文的其余部分介绍了绑定机制以及它如何适用于每个版本的 SQL Server。

> [!NOTE]
> 绑定适用于 (数据库内) 仅绑定到 SQL Server 实例的实例。 绑定与 (独立) 安装无关。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**SQL Server 2017 绑定注意事项**

对于 SQL Server 机器学习服务, 你可以考虑仅在 Microsoft Machine Learning Server 开始为你已有的内容提供其他包或较新版本时进行绑定。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 绑定注意事项**

对于 SQL Server 2016 R 服务客户, 绑定提供更新的 R 包、不属于原始安装 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) 和[预先训练模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)的新包, 所有这些都可以在每个新的主要和次要版本的[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。 绑定不提供 Python 支持, 这是一项 SQL Server 2017 功能。
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>版本映射

下表是一个版本映射, 其中显示了跨 release 车辆的包版本, 以便你可以在绑定到 Microsoft Machine Learning Server (以前称为 R Server, 在开始添加 Python 支持之前确定可能的升级路径在 MLS 9.2.1 中)。 

请注意, 绑定不保证最新版本的 R 或 Anaconda。 绑定到 Microsoft Machine Learning Server (MLS) 时, 会通过安装程序安装 R 或 Python 版本, 这可能不是 web 上提供的最新版本。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

组件 |初始版本 | [R Server 9.0。1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9。1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) over R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[预先训练模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server 机器学习服务**](../install/sql-machine-learning-services-windows-install.md)

组件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) over R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 over Python 3。5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[预先训练模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>组件升级的工作原理 

将 R 和 Python 的现有安装绑定到 Machine Learning Server 时, 会升级 r 和 Python 库和可执行文件。 当你在具有 R 或 Python 集成的现有 SQL Server 数据库引擎实例上运行安装程序时, [Microsoft Machine Learning Server 安装程序](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)将执行绑定。 安装程序将检测现有功能并提示您重新绑定到 Machine Learning Server。 

在绑定期间, 和的`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` `C:\Program Files\Microsoft\ML Server\R_SERVER`新`\PYTHON_SERVICES`的`\PYTHON_SERVER`可执行文件和库将覆盖和的内容。

同时, 维护模型还会从 SQL Server 更新机制翻转到 Microsoft Machine Learning Server 的主要和次要发布周期。 对于需要更高版本的生成 R 和 Python 模块以获得其解决方案的数据科学团队而言, 切换支持策略是一个不错的选择。 

+ 如果未绑定, 则在安装 SQL Server Service Pack 或累积更新 (CU) 时, 将为 bug 修复修补 R 和 Python 包。 
+ 通过绑定, 可以将较新的包版本应用于你的实例, 而不是在新的[生命周期策略](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和 Microsoft Machine Learning Server 版本下独立于 CU 发布计划。 新式生命周期支持策略在一年较短的有效期内提供更频繁的更新。 后期绑定后, 可以继续使用 MLS 安装程序, 以便在 Microsoft 下载站点上提供的 R 和 Python 的将来更新。

仅适用于 R 和 Python 功能的绑定。 也就是说, 适用于 R 和 Python 功能的开源包 (Microsoft R Open、Anaconda) 以及专有包 RevoScaleR、revoscalepy, 等等。 绑定不会更改数据库引擎实例的支持模型, 也不会更改 SQL Server 的版本。

绑定是可逆的。 你可以通过取消[绑定实例](#bkmk_Unbind)并 reparing 你的 SQL Server 数据库引擎实例, 恢复到 SQL Server 服务。

汇总时, 绑定的步骤如下所示:

+ 从已配置的现有 SQL Server R Services 或 SQL Server 机器学习服务开始。
+ 确定要使用的升级组件的 Microsoft Machine Learning Server 版本。
+ 下载并运行该版本的安装程序。 安装程序检测到现有的实例, 添加绑定选项, 并返回兼容实例的列表。
+ 选择要绑定的实例, 然后完成安装程序以执行绑定。

就用户体验而言, 该技术以及使用它的方式没有变化。 唯一的区别在于是否存在更新版本的包, 并且可能不会通过 SQL Server 初始提供其他包。

## <a name="bkmk_BindWizard"></a>使用安装程序绑定到 MLS

Microsoft 机器学习安装程序将检测现有功能并 SQL Server 版本, 并调用名为 SqlBindR 的实用工具来更改绑定。 在内部, SqlBindR 链接到安装并间接使用。 稍后, 你可以从命令行直接调用 SqlBindR 来执行特定的选项。

1. 在 SSMS 中, `SELECT @@version`运行以验证服务器是否满足最低生成要求。 

   对于 SQL Server 2016 R 服务, 最小为[Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)和[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 检查 R 基包和 RevoScaleR 包的版本, 以确认现有版本是否低于你计划将其替换为的版本。 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. 关闭 SSMS 以及与 SQL Server 的打开连接的任何其他工具。 绑定将覆盖程序文件。 如果 SQL Server 有打开的会话, 则绑定将失败, 并出现绑定错误代码6。

1. 将 Microsoft Machine Learning Server 下载到包含要升级的实例的计算机上。 建议采用[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解压缩文件夹, 然后启动位于 MLSWIN93 下的 ServerSetup。

   ![Microsoft Machine Learning Server 安装向导](media/mls-921-installer-start.PNG)

1. 在 "**配置安装**" 中, 确认要升级的组件, 并查看兼容实例的列表。 

   此步骤非常重要。

   在左侧, 选择要保留或升级的每个功能。 不能升级某些功能而不是其他功能。 如果为空复选框, 则将删除该功能 (假定当前已安装)。 在屏幕截图中, 提供了一个 SQL Server 2016 R Services (MSSQL13.MSSQLSERVER) 的实例, 并选择了预训练模型的 r 版本。 此配置有效, 因为 SQL Server 2016 支持 R 但不支持 Python。

   如果要在 SQL Server 2016 R Services 上升级组件, 请不要选择 Python 功能。 不能将 Python 添加到 SQL Server 2016 R Services 中。

   在右侧, 选择实例名称旁边的复选框。 如果未列出任何实例, 则你的组合不兼容。 如果未选择实例, 将创建 Machine Learning Server 的新独立安装, 并且 SQL Server 库保持不变。 如果无法选择实例, 则它可能不在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![配置安装步骤](media/mls-931-installer-mssql13.png)

1. 在 "**许可协议**" 页上, 选择 "**我接受这些条款**" 以接受 Machine Learning Server 的许可条款。 

1. 在连续页面上, 为所选的任何开源组件 (例如 Microsoft R Open 或 Python Anaconda 分发) 提供其他许可条件。

1. 在 "**几乎**" 页上, 记下 "安装" 文件夹。 默认文件夹为 \Program Files\Microsoft\ML Server。

    如果要更改安装文件夹, 请单击 "**高级**" 以返回到向导的第一页。 但是, 必须重复前面的所有选择。

在安装过程中, 将替换 SQL Server 使用的任何 R 或 Python 库, 并更新快速启动板以使用较新的组件。 因此, 如果实例以前使用的是默认 R_SERVICES 文件夹中的库, 则在升级之后, 将删除这些库, 并将快速启动板服务的属性更改为使用新位置中的库。

绑定会影响这些文件夹的内容:C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 替换为 C:\Program Files\Microsoft\ML Server\R_SERVER. 的内容。 第二个文件夹及其内容由 Microsoft Machine Learning Server 安装程序创建。 

如果升级失败, 请检查[SqlBindR 错误代码](#sqlbindr-error-codes)以了解详细信息。

## <a name="confirm-binding"></a>确认绑定

重新检查 R 和 RevoScaleR 的版本, 以确认是否有更新的版本。 使用与数据库引擎实例中的 R 包一起分发的 R 控制台来获取包信息:

```sql
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

对于绑定到 Machine Learning Server 9.3 SQL Server 2016 R 服务, R 基包应为 3.4.3, RevoScaleR 应为 9.3, 还应具有 MicrosoftML 9.3。 

如果已添加预先训练的模型, 这些模型将嵌入到 MicrosoftML 库中, 可以通过 MicrosoftML 函数调用它们。 有关详细信息, 请参阅[MicrosoftML 的 R 示例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>脱机绑定 (无 internet 访问)

对于没有 internet 连接的系统, 你可以将安装程序和 .cab 文件下载到连接到 internet 的计算机, 然后将文件传输到隔离服务器。 

安装程序 (ServerSetup) 包括 Microsoft 包 (RevoScaleR、MicrosoftML、olapR、sqlRUtils)。 .Cab 文件提供其他核心组件。 例如, "SRO" cab 提供 R Open, 即 Microsoft 的开放源代码 R 分发版。

以下说明介绍了如何将文件放入脱机安装。

1. 下载 MLS 安装程序。 它下载为一个压缩文件。 建议采用[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), 但也可以安装[早期版本](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下载 .cab 文件。 以下链接适用于9.3 版本。 如果需要早期版本, 可在[R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)中找到其他链接。 请记住, Python/Anaconda 只能添加到 SQL Server 机器学习服务实例。 适用于 R 和 Python 的预先训练的模型.cab 提供您正在使用的语言的模型。

    | 功能 | 下载 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 预定型模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 将 .zip 和 .cab 文件传输到目标服务器。

1. 在服务器上, 键入`%temp%` "运行" 命令以获取 temp 目录的物理位置。 物理路径因计算机而异, 但通常`C:\Users\<your-user-name>\AppData\Local\Temp`是。

1. 将 .cab 文件放在% temp% 文件夹中。

1. 解压缩安装程序。

1. 运行 ServerSetup 并按照屏幕上的提示完成安装。

## <a name="bkmk_BindCmd"></a>命令行操作

运行 Microsoft Machine Learning Server 后, 可以使用名为 SqlBindR 的命令行实用程序来进行进一步的绑定操作。 例如, 如果您决定反转绑定, 则可以重新运行安装程序, 也可以使用命令行实用工具。 此外, 还可以使用此工具检查实例兼容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 您可能尚未运行安装程序。 SqlBindR 仅在运行 Machine Learning Server 安装程序之后才可用。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置为 C:\Program Files\Microsoft\MLServer\Setup

2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如, 实例名称可能是 MSSQL14.MSSQLSERVER 用于默认实例, 或类似于 SERVERNAME。MYNAMEDINSTANCE.

3. 使用 */bind*参数运行**SqlBindR**命令, 并使用上一步中返回的实例名称指定要升级的实例的名称。

   例如, 若要升级默认实例, 请键入:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 升级完成后, 重新启动与任何已修改的实例关联的启动板服务。

## <a name="bkmk_Unbind"></a>恢复或取消绑定实例

可以通过 SQL Server 安装程序建立的 R 和 Python 组件的初始安装来还原绑定实例。 有三个部分要恢复到 SQL Server 服务。

+ [步骤 1：从 Microsoft Machine Learning Server 取消绑定](#step-1-unbind)
+ [步骤 2：将实例还原为原始状态](#step-2-restore)
+ [步骤 3：重新安装添加到安装的所有包](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步骤 1：首先

可以使用两个选项来回滚绑定: 重新运行安装程序或使用 SqlBindR 命令行实用工具。

#### <a name="bkmk_wizunbind"></a>使用安装程序取消绑定

1. 找到 Machine Learning Server 的安装程序。 如果已删除安装程序, 则可能需要再次下载该安装程序, 或从另一台计算机复制它。
2. 请确保在包含要取消绑定的实例的计算机上运行该安装程序。
2. 安装程序标识用于取消绑定的本地实例。
3. 取消选中要恢复为原始配置的实例旁边的复选框。
4. 接受许可协议。 即使在安装时, 也必须指明接受许可条款。
5. 单击 **“完成”** 。 此过程将使用一段时间。

#### <a name="bkmk_cmdunbind"></a>使用命令行取消绑定

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如, 以下命令将还原默认实例:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步骤 2：修复 SQL Server 实例

运行 SQL Server 安装程序以修复具有 R 和 Python 功能的数据库引擎实例。 现有更新将保留, 但如果你错过了对 R 和 Python 包的任何 SQL Server 服务更新, 则此步骤将应用这些修补程序。

另外, 这也是更好的工作, 但您也可以完全卸载并重新安装数据库引擎实例, 然后应用所有服务更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步骤 3：添加任何第三方包

你可能已将其他开源或第三方包添加到包库。 由于反向绑定会切换默认包库的位置, 因此你必须将包重新安装到 R 和 Python 现在使用的库。 有关详细信息, 请参阅[R 包信息](../package-management/r-package-information.md)和[安装](../package-management/install-additional-r-packages-on-sql-server.md), 以及[Python 包信息](../package-management/python-package-information.md)和[安装](../package-management/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR 命令语法

### <a name="usage"></a>用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameters

|“属性”|Description|
|------|------|
|*list*| 显示当前计算机上所有 SQL 数据库实例 ID 的列表|
|*bind*| 将指定的 SQL 数据库实例升级至 R Server 最新版本，并确保实例会自动获取 R Server 的未来升级|
|*unbind*|从指定的 SQL 数据库实例中卸载 R Server 最新版本，并防止未来 R Server 升级影响该实例|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>绑定错误

MLS 安装程序和 SqlBindR 都返回以下错误代码和消息。

|错误代码  | 消息           | 详细信息               |
|------------|-------------------|-----------------------|
|绑定错误0 | 正常 (成功) | 绑定已传递且没有错误。 |
|绑定错误1 | 参数无效 | 语法错误。 |
|绑定错误2 | 无效操作 | 语法错误。 |
|绑定错误3 | 实例无效 | 实例存在, 但对于绑定无效。 |
|绑定错误4 | 不可绑定 | |
|绑定错误5 | 已绑定 | 已运行 *bind* 命令，但指定的实例已绑定。 |
|绑定错误6 | 绑定失败 | 取消绑定实例时出错。 如果在不选择任何功能的情况下运行 MLS 安装程序, 则会发生此错误。 绑定要求您同时选择 MSSQL 实例和 R 和 Python, 前提是该实例为 2017 SQL Server。 当 SqlBindR 无法写入 Program Files 文件夹时, 也会发生此错误。 打开会话或句柄 SQL Server 会导致发生此错误。 如果收到此错误, 请重新启动计算机, 并在启动任何新会话之前重做绑定步骤。|
|绑定错误7 | 未绑定 | 数据库引擎实例具有 R Services 或 SQL Server 机器学习服务。 实例未绑定到 Microsoft Machine Learning Server。 |
|绑定错误8 | 取消绑定失败 | 取消绑定实例时出错。 |
|绑定错误9 | 未找到任何实例 | 在此计算机上找不到数据库引擎实例。 |

## <a name="known-issues"></a>已知问题

本部分列出了特定于使用 SqlBindR 实用程序的已知问题, 或对可能影响 SQL Server 实例的 Machine Learning Server 的升级。

### <a name="restoring-packages-that-were-previously-installed"></a>正在还原以前安装的包

如果已升级到 Microsoft R Server 9.0.1, 则该版本的 SqlBindR 版本无法完全还原原始包或 R 组件, 要求用户在实例上运行 SQL Server repair, 应用所有服务版本, 然后重新启动实例。

更高版本的 SqlBindR 自动还原原始 R 功能, 无需重新安装 R 组件或重新修补服务器。 但是, 必须安装在初始安装后可能已添加的任何 R 包更新。

如果你使用了包管理角色来安装和共享包, 则此任务要容易得多: 可以使用 R 命令将已安装的包与数据库中的记录同步到文件系统, 反之亦然。 有关详细信息, 请参阅[SQL Server 的 R 包管理](../r/install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server 的多个升级的问题

如果以前已将 SQL Server 2016 R Services 的实例升级到 9.0.1, 则当你为 Microsoft R Server 9.1.0 运行新的安装程序时, 它将显示所有有效实例的列表, 然后, 默认情况下会选择以前绑定的实例。 如果继续, 则之前绑定的实例是未绑定的。 因此, 会删除之前的9.0.1 版安装 (包括所有相关包), 但不会安装 Microsoft R Server 的新版本 (9.1.0)。

作为一种解决方法, 你可以修改现有的 R Server 安装, 如下所示:
1. 在 "控制面板" 中, 打开 "**添加或删除程序**"。
2. 找到 Microsoft R Server, 然后单击 "**更改/修改**"。
3. 当安装程序启动时, 选择要绑定到9.1.0 的实例。

Microsoft Machine Learning Server 9.2.1 和9.3 没有此问题。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定会保留多个临时文件夹

有时, 绑定和取消绑定操作无法清理临时文件夹。
如果发现文件夹的名称如下所示, 可以在安装完成后将其删除:R_SERVICES_<guid>

> [!NOTE]
> 请确保等待安装完成。 删除与某个版本关联的 R 库可能需要较长时间, 然后添加新的 R 库。 操作完成后, 将删除临时文件夹。

## <a name="see-also"></a>另请参阅

+ [安装适用于 Windows 的 Machine Learning Server (Internet 连接)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安装适用于 Windows 的 Machine Learning Server (脱机)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server 中的已知问题](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [以前版本的 R Server 中的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [弃用、已停用或更改的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
