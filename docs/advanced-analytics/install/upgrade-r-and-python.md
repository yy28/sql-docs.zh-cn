---
title: 升级 R 和 Python 组件
description: 使用 sqlbindr.exe 绑定到 Machine Learning Server，以升级 SQL Server 机器学习服务或 SQL Server R Services 中的 R 和 Python。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634552"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升级 SQL Server 实例中的机器学习（R 和 Python）组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 中的 R 和 Python 集成包括开放源代码和 Microsoft 专有包。 在标准 SQL Server 服务下，将根据 SQL Server 发布周期更新包，并提供针对当前版本中现有包的 bug 修补程序，但不升级主要版本。 

不过，许多数据科学家习惯于在可用时使用较新的包。 对于 SQL Server 机器学习服务（数据库内）和 SQL Server R Services（数据库内），可以通过绑定到“Microsoft Machine Learning Server”来获得[更新版本的 R 和 Python](#version-map)   。 

## <a name="what-is-binding"></a>什么是绑定？

绑定是一个安装过程，它将 R_SERVICES 和 PYTHON_SERVICES 文件夹中的内容替换为 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index) 中较新的可执行文件、库和工具。

随着组件的更新，服务模式也发生了变化。 有了 [SQL Server 累积更新](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)，服务更新现在符合[现代生命周期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)上 [Microsoft R Server 和 Machine Learning Server 的支持时间线](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)，而不是 [SQL Server 产品生命周期](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)。

除了组件版本和服务更新之外，绑定不会更改基础安装：R 和 Python 集成仍是数据库引擎实例的一部分，许可没有改变（没有与绑定相关的额外成本），SQL Server 支持策略仍然适用于数据库引擎。 本文的其余部分将介绍绑定机制以及它如何用于 SQL Server 的每个版本。

> [!NOTE]
> 绑定仅适用于绑定到 SQL Server 实例的（数据库内）实例。 绑定与（独立）安装无关。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**SQL Server 2017 绑定注意事项**

对于 SQL Server 机器学习服务，只有当 Microsoft Machine Learning Server 开始在现有基础上提供其他包或更新版本时，才考虑绑定。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**SQL Server 2016 绑定注意事项**

对于 SQL Server 2016 R Services 客户，绑定提供了更新的 R 包、不属于原始安装的新包 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) 和[预定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)，可在 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index) 的每个新的主要和次要版本中进一步刷新所有这些内容。 绑定不提供 Python 支持，这是 SQL Server 2017 具有的功能。
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>版本映射

下表是一个版本映射，显示了跨发行工具的包版本，以便在绑定到 Microsoft Machine Learning Server（从 MLS 9.2.1 开始添加 Python 支持之前称为 R Server）时确定潜在的升级路径。 

请注意，绑定不能保证提供最新版本的 R 或 Anaconda。 绑定到 Microsoft Machine Learning Server (MLS) 时，将通过安装程序安装 R 或 Python 版本，这可能不是 Web 上提供的最新版本。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

组件 |初始版本 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
R 上的 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[预定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server 机器学习服务**](../install/sql-machine-learning-services-windows-install.md)

组件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
R 上的 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Python 3.5 上的 Anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[预定型模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>组件升级的工作原理 

将现有的 R 和 Python 安装绑定到 Machine Learning Server 时，会升级 R 和 Python 库和可执行文件。 在现有的具有 R 或 Python 集成的 SQL Server 数据库引擎实例上运行安装程序时，由 [Microsoft Machine Learning Server 安装程序](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)执行绑定。 安装程序会检测现有功能并提示你重新绑定到 Machine Learning Server。 

在绑定期间，`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` 和 `\PYTHON_SERVICES` 的内容将被 `C:\Program Files\Microsoft\ML Server\R_SERVER` 和 `\PYTHON_SERVER` 的更新的可执行文件和库覆盖。

同时，服务模式也从 SQL Server 更新机制转变为 Microsoft Machine Learning Server 更频繁的主要和次要版本周期。 对于需要新一代 R 和 Python 模块作为解决方案的数据科学团队来说，切换支持策略是一项具有吸引力的选择。 

+ 如果没有绑定，在安装 SQL Server 服务包或累积更新 (CU) 时，会修补 R 和 Python 包以修复 bug。 
+ 借助绑定，可以根据[现代生命周期策略](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和 Microsoft Machine Learning Server 版本，可独立于 CU 发布计划将较新的包版本应用于实例。 现代生命周期支持策略在较短的一年生命期内提供更频繁的更新。 绑定后，将继续使用 MLS 安装程序来更新 R 和 Python，因为它们在 Microsoft 下载站点上可用。

绑定仅适用于 R 和 Python 功能。 也就是说，适用于 R 和 Python 功能的开放源代码包（Microsoft R open、Anaconda）以及 RevoScaleR、revoscalepy 等专有包。 绑定不会更改数据库引擎实例的支持模型，也不会更改 SQL Server 的版本。

绑定是可逆操作。 通过[取消绑定实例](#bkmk_Unbind)并修复 SQL Server 数据库引擎实例，可以还原为 SQL Server 服务。

综上所述，绑定的步骤如下所示：

+ 从已配置的现有 SQL Server R Services 或 SQL Server 机器学习服务安装开始。
+ 确定哪个版本的 Microsoft Machine Learning Server 具有要使用的升级组件。
+ 下载并运行该版本的安装程序。 安装程序将检测现有实例，添加绑定选项，然后返回兼容实例的列表。
+ 选择要绑定的实例，然后完成设置以执行绑定。

就用户体验而言，技术及其使用方式是不变的。 唯一的区别在于存在较新版本的包，并且可能存在最初无法通过 SQL Server 提供的其他包。

## <a name="bkmk_BindWizard"></a>使用安装程序绑定到 MLS

Microsoft 机器学习安装程序检测现有功能和 SQL Server 版本，并调用名为 SqlBindR.exe 的实用工具来更改绑定。 在内部，SqlBindR 被链接到安装程序并间接使用。 稍后，可以直接从命令行调用 SqlBindR 来执行特定选项。

1. 在 SSMS 中，运行 `SELECT @@version` 以验证服务器是否满足最低版本要求。 

   对于 SQL Server 2016 R Services，最低版本为 [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) 和 [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 检查 R 基础版本和 ReVoSalcER 包版本，以确认现有版本低于计划替换的版本。 

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

1. 关闭 SSMS 和任何与 SQL Server 具有开放连接的其他工具。 绑定将覆盖程序文件。 如果 SQL Server 有打开的会话，则绑定将失败，显示绑定错误代码 6。

1. 将 Microsoft Machine Learning Server 下载到包含要升级的实例的计算机上。 我们推荐[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解压缩文件夹并启动位于 MLSWIN93 下的 ServerSetup.exe。

   ![Microsoft Machine Learning Server 安装向导](media/mls-921-installer-start.PNG)

1. 在“配置安装”上，确认要升级的组件，并查看兼容实例的列表  。 

   此步骤非常重要。

   在左侧，选择要保留或升级的每个功能。 无法升级某些功能，但可升级其他功能。 如果当前已安装该功能，则不勾选复选框会将其删除。 在屏幕截图中，以 SQL Server 2016 R Services (MSSQL13) 的实例为例，选择了 R 和 R 版本的预定型模型。 此配置有效，因为 SQL Server 2016 支持 R，但不支持 Python。

   如果要升级 SQL Server 2016 R Services 上的组件，请勿选择 Python 功能。 无法将 Python 添加到 SQL Server 2016 R Services 中。

   在右侧，选中实例名称旁边的复选框。 如果未列出任何实例，则说明组合不兼容。 如果不选择实例，将创建新的 Machine Learning Server 独立安装，并且 SQL Server 库保持不变。 如果无法选择实例，则该实例可能不位于 [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1) 中。 

    ![配置安装步骤](media/mls-931-installer-mssql13.png)

1. 在“许可协议”页面上，选择“我接受这些条款”以接受 Machine Learning Server 的许可条款   。 

1. 在后续页面中，同意所选的任何开源组件（如 Microsoft R open 或 Python Anaconda 分发版）的其他许可条件。

1. 在“即将完成”页面上，记下安装文件夹  。 默认文件夹为 \Program Files\Microsoft\ML Server。

    如果要更改安装文件夹，请单击“高级”以返回向导首页  。 但是，必须重复选择前面的所有选择内容。

在安装过程中，将替换 SQL Server 使用的任何 R 或 Python 库，并更新启动板以使用更新的组件。 因此，如果实例以前使用过默认 R_SERVICES 文件夹中的库，则在升级之后删除这些库，并更改启动板服务的属性以使用新位置中的库。

绑定会影响这些文件夹的内容：C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library 的内容替换为 C:\Program Files\Microsoft\ML Server\R_SERVER 的内容。 第二个文件夹及其内容由 Microsoft Machine Learning Server 安装程序创建。 

如果升级失败，请检查 [SqlBindR 错误代码](#sqlbindr-error-codes)以获取详细信息。

## <a name="confirm-binding"></a>确认绑定

重新检查 R 和 RevoScaleR 的版本，以确认是否有更新的版本。 使用与数据库引擎实例中的 R 包一起分发的 R 控制台，以获取包信息：

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

对于绑定到 Machine Learning Server 9.3 的 SQL Server 2016 R Services，R 基程序包应为 3.4.3，RevoScaleR 应为 9.3，并且还应具有 MicrosoftML 9.3。 

如果添加了预定型模型，这些模型将嵌入到 MicrosoftML 库中，可以通过 MicrosoftML 函数调用它们。 有关详细信息，请参阅 [MicrosoftML 的 R 示例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>脱机绑定（无 internet 访问）

对于没有 Internet 连接的系统，可以将安装程序和 .cab 文件下载到已连接 Internet 的计算机上，然后将文件传输到独立服务器。 

安装程序 (ServerSetup.exe) 包括 Microsoft 包（RevoScaleR、MicrosoftML、olapR、sqlRUtils）。 .cab 文件提供其他核心组件。 例如，“SRO”cab 提供了 R Open，这是 Microsoft 的开放源代码 R 分发版。

以下说明解释如何放置文件以进行脱机安装。

1. 下载 MLS 安装程序。 它以单个压缩文件的形式下载。 我们推荐[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但也可以安装[早期版本](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下载 .cab 文件。 以下链接适用于 9.3 版本。 如果需要早期版本，可以在 [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components) 中找到其他链接。 请记住，Python/Anaconda 只能添加到 SQL Server 机器学习服务实例中。 预定型模型适用于 R 和 Python；.cab 以正在使用的语言提供模型。

    | 功能 | 下载 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 预定型模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 将 .zip 和 .cab 文件传输到目标服务器。

1. 在服务器上，在 Run 命令中键入 `%temp%` 以获取临时目录的物理位置。 物理路径因计算机而异，但通常是 `C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 将 .cab 文件放在 %temp% 文件夹中。

1. 解压缩安装程序。

1. 运行 ServerSetup.exe 并按照屏幕提示完成安装。

## <a name="bkmk_BindCmd"></a>命令行操作

运行 Microsoft Machine Learning Server 后，名为 SqlBindR.exe 的命令行实用工具可用于进行进一步的绑定操作。 例如，如果决定反转绑定，可以重新运行安装程序或使用命令行实用工具。 此外，还可以使用此工具检查实例兼容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 可能尚未运行安装程序。 只有在运行 Machine Learning Server 安装程序之后，SqlBindR 才可用。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置为 C:\Program Files\Microsoft\MLServer\Setup

2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如，对于默认实例，实例名称可能是 MSSQL14.MSSQLSERVER，或者类似于 SERVERNAME.MYNAMEDINSTANCE。

3. 使用 /bind 参数运行 SqlBindR.exe 命令，并使用上一步中返回的实例名称指定要升级的实例的名称   。

   例如，若要升级默认实例，请键入：`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 在升级完成后，重启与已修改的任何实例关联的启动板服务。

## <a name="bkmk_Unbind"></a>还原或取消绑定实例

可以将绑定实例还原为由 SQL Server 安装程序建立的 R 和 Python 组件的初始安装。 要还原到 SQL Server 服务，需执行三个步骤。

+ [步骤 1：从 Microsoft Machine Learning Server 取消绑定](#step-1-unbind)
+ [步骤 2：将实例还原为原始状态](#step-2-restore)
+ [步骤 3：重新安装添加到安装的所有包](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步骤 1：取消绑定

回滚绑定有两个选项：再次重新运行安装程序或使用 SqlBindR 命令行实用工具。

#### <a name="bkmk_wizunbind"></a> 使用安装程序取消绑定

1. 找到 Machine Learning Server 的安装程序。 如果已删除该安装程序，可能需要重新下载，或从另一台计算机复制。
2. 请确保在包含要取消绑定的实例的计算机上运行安装程序。
2. 安装程序将标识要取消绑定的本地实例。
3. 取消选中要还原为原始配置的实例旁边的复选框。
4. 接受许可协议。 即使在安装时也必须表明你已接受许可条款。
5. 单击 **“完成”** 。 此过程需要花费一点时间。

#### <a name="bkmk_cmdunbind"></a> 使用命令行取消绑定

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如，以下命令将还原默认实例：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步骤 2：修复 SQL Server 实例

运行 SQL Server 安装程序以修复具有 R 和 Python 功能的数据库引擎实例。 现有的更新将保留，但是如果你忘记了对 R 和 Python 包的任何 SQL Server 服务更新，则此步骤将应用这些修补程序。

或者，虽然会进行更多操作，但也可以完全卸载并重新安装数据库引擎实例，然后应用所有服务更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步骤 3：添加任何第三方包

你可能已将其他开放源代码或第三方包添加到包库中。 由于反向绑定会切换默认包库的位置，因此必须将包重新安装到 R 和 Python 正在使用的库中。 有关详细信息，请参阅 [R 包信息](../package-management/r-package-information.md)和[安装](../package-management/install-additional-r-packages-on-sql-server.md)，以及 [Python 包信息](../package-management/python-package-information.md)和[安装](../package-management/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令语法

### <a name="usage"></a>用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameters

|“属性”|描述|
|------|------|
|*list*| 显示当前计算机上所有 SQL 数据库实例 ID 的列表|
|*bind*| 将指定的 SQL 数据库实例升级至 R Server 最新版本，并确保实例会自动获取 R Server 的未来升级|
|*unbind*|从指定的 SQL 数据库实例中卸载 R Server 最新版本，并防止未来 R Server 升级影响该实例|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>绑定错误

MLS 安装程序和 SqlBindR 都返回以下错误代码和消息。

|错误代码  | 消息           | 详细信息               |
|------------|-------------------|-----------------------|
|绑定错误 0 | 确定（成功） | 绑定已传递，未出错。 |
|绑定错误 1 | 参数无效 | 语法错误。 |
|绑定错误 2 | 操作无效 | 语法错误。 |
|绑定错误 3 | 无效实例 | 实例存在，但对于绑定无效。 |
|绑定错误 4 | 不可绑定 | |
|绑定错误 5 | 已绑定 | 已运行 *bind* 命令，但指定的实例已绑定。 |
|绑定错误 6 | 绑定失败 | 取消绑定实例时出错。 如果在未选择任何功能的情况下运行 MLS 安装程序，则可能发生此错误。 绑定要求同时选择 MSSQL 实例、R 和 Python，前提是该实例为 SQL Server 2017。 如果 SqlBindR 无法写入“程序文件”文件夹，也会发生此错误。 打开 SQL Server 的会话或句柄将导致发生此错误。 如果出现此错误，请重启计算机并在启动任何新会话之前重新执行绑定步骤。|
|绑定错误 7 | 未绑定 | 数据库引擎实例具有 R 服务或 SQL Server 机器学习服务。 实例未绑定到 Microsoft Machine Learning Server。 |
|绑定错误 8 | 取消绑定失败 | 取消绑定实例时出错。 |
|绑定错误 9 | 未找到任何实例 | 在此计算机上找不到数据库引擎实例。 |

## <a name="known-issues"></a>已知问题

本部分列出特定于使用 SqlBindR.exe 实用工具或升级可能影响 SQL Server 实例的 Machine Learning Server 的已知问题。

### <a name="restoring-packages-that-were-previously-installed"></a>还原以前安装的包

如果已升级到 Microsoft R Server 9.0.1，适用于该版本的 SqlBindR.exe 版本无法完全还原初始包或 R 组件，需要用户在实例上运行 SQL Server 修复，应用所有服务版本，然后重新启动实例。

更高版本的 SqlBindR 会自动还原初始的 R 功能，无需重新安装 R 组件或重新修补服务器。 但是，必须安装在初始安装之后可能添加的任何 R 包更新。

如果已使用包管理角色来安装和共享包，则此任务要简单得多：可以使用 R 命令和数据库中的记录将已安装的包同步到文件系统，反之亦然。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../r/install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>从 SQL Server 进行多次升级时出现的问题

如果之前已将 SQL Server 2016 R Services 的实例升级到 9.0.1，则在运行 Microsoft R Server 9.1.0 的新安装程序时，它将显示所有有效实例的列表，然后默认选择以前绑定的实例。 如果继续操作，将取消绑定以前绑定的实例。 因此，会删除先前的 9.0.1 安装，包括任何相关的包，但是不安装新版本的 Microsoft R Server (9.1.0)。

作为解决方案，可以修改现有的 R Server 安装，如下所示：
1. 在“控制面板”中，打开“添加或删除程序”  。
2. 找到 Microsoft R Server，然后单击“更改/修改”  。
3. 当安装程序启动时，选择要绑定到 9.1.0 的实例。

Microsoft Machine Learning Server 9.2.1 和 9.3 没有此问题。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定会保留多个临时文件夹

有时，绑定和取消绑定操作无法清理临时文件夹。
如果发现具有此类名称的文件夹，可以在安装完成后将其删除：R_SERVICES_<guid>

> [!NOTE]
> 请确保等待安装完成。 删除与某个版本关联的 R 库，然后添加新的 R 库可能需要很长时间。 操作完成后，将删除临时文件夹。

## <a name="see-also"></a>另请参阅

+ [安装适用于 Windows 的 Machine Learning Server（已连接 Internet）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安装适用于 Windows 的 Machine Learning Server（脱机）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Machine Learning Server 中的已知问题](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [R Server 早期版本的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已弃用、已中断或已更改的功能](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
