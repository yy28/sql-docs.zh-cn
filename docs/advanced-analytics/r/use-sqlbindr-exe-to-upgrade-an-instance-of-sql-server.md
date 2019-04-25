---
title: 升级 R 和 Python 组件的 SQL Server 机器学习服务
description: 升级 R 和 Python 在 SQL Server 2016 Services 或 SQL Server 2017 机器学习服务使用 sqlbindr.exe 绑定到机器学习服务器中。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: da28d6f0ae423ce9cca0c6d571af944a2d7acd3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642052"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升级 SQL Server 实例中的机器学习 （R 和 Python） 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server中的R和Python集成包括开源代码和Microsoft专有包。 在标准SQL Server服务框架下，是根据SQL Server发布周期来更新包的，同时提供针对当前版本中现有包错误的修复程序，但不存在主要版本升级。 

但是，许多数据科学家习惯于使用较新的包可用。 有关 SQL Server 2017 机器学习服务 （数据库内） 和 SQL Server 2016 R Services （数据库内），可以获取[较新版本的 R 和 Python](#version-map)通过*绑定*到**Microsoft机器学习服务器**。 

## <a name="what-is-binding"></a>什么绑定？

绑定是交换出使用较新的可执行文件，库，R_SERVICES 和 PYTHON_SERVICES 文件夹的内容和工具的安装流程[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。

与更新的组件是为模型中的交换机。 而不是[SQL Server 产品生命周期](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)，使用[SQL Server 累积更新](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions)，你的服务更新现在符合[Microsoft R Server （& a） 计算机的支持时间线学习 Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)上[现代生命周期](https://support.microsoft.com/help/30881/modern-lifecycle-policy)。

组件版本和服务更新，除了绑定不会更改您的安装的基础知识：R 和 Python 集成仍然是数据库引擎实例的一部分许可不变的 （无额外成本与绑定相关联），和 SQL Server 支持策略仍保留为数据库引擎。 本文的其余部分介绍的绑定机制及其使用方式的每个版本的 SQL Server。

> [!NOTE]
> 绑定适用于仅它们被绑定到 SQL Server 实例 （数据库内） 实例。 绑定不相关 （独立版） 安装。

**SQL Server 2017 绑定注意事项**

为 SQL Server 2017 机器学习服务，将 Microsoft Machine Learning Server 开始提供的其他包或通过您的较新版本已有时只考虑绑定。

**SQL Server 2016 绑定注意事项**

对于 SQL Server 2016 R Services 的客户，绑定提供更新后的 R 包，新的包不是原始安装的一部分 ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package))，并[预先训练模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)，所有这些可进一步在每个新的主版本号和次版本的刷新[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index)。 绑定未提供 Python 支持，后者是 SQL Server 2017 功能。 

<a name="version-map"></a>

## <a name="version-map"></a>版本映射

下表是版本映射时，显示的包版本发布途径，以便 Microsoft 机器学习服务器 （以前称为 R Server 之前启动的 Python 支持添加到绑定时，可以确定潜在的升级路径在 MLS 9.2.1)。 

请注意，绑定不能保证的最新版本的 R 或 Anaconda。 将绑定到 Microsoft 机器学习服务器 (MLS)，可以获取安装执行安装程序，这可能不会在 web 上找到可用的最新版本的 R 或 Python 版本。

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

组件 |初始版本 | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
通过 R 的 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[预先训练的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 2017 机器学习服务**](../install/sql-machine-learning-services-windows-install.md)

组件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
通过 R 的 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
通过 Python 3.5 anaconda 4.2  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[预先训练的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>组件升级的工作原理 

R 和 Python 库和可执行文件将升级现有安装的 R 和 Python 绑定到机器学习服务器时。 绑定执行者[Microsoft 机器学习服务器安装程序](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)现有 SQL Server 数据库引擎实例上，2016年或 2017 中，运行安装程序时具有 R 或 Python 集成。 安装程序检测到的现有功能，并提示您重新绑定到 Machine Learning Server。 

在绑定中，C:\Program Files\Microsoft SQL Server\MSSQL14 的内容。MSSQLSERVER\R_SERVICES 和 \PYTHON_SERVICES 会覆盖较新的可执行文件和 C:\Program Files\Microsoft\ML Server\R_SERVER 和 \PYTHON_SERVER 的库。

同时，维护服务模型还翻转从 SQL Server 更新机制到的 Microsoft Machine Learning Server 更频繁的主版本号和次版本周期。 切换的支持策略是个不错的选择的数据科学团队需要更高版本生成 R 和 Python 模块对其解决方案。 

+ 没有绑定，R 和 Python 包安装 SQL Server service pack 或累积更新 (CU) 时的 bug 修复修补。 
+ 使用绑定，则较新的包版本可应用于您的实例，不考虑 CU 版本计划下[Modern Lifecycle 策略](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和版本的 Microsoft Machine Learning Server。 现代生命周期支持策略相比更短、 一年使用期限更频繁的更新。 后期绑定，您将继续使用 R 和 Python 的将来更新 MLS 安装程序，如 Microsoft 下载站点上可用。

绑定适用于 R 和 Python 功能。 也就是说，对 R 和 Python 功能 （Microsoft R Open，Anaconda） 和专有的开放源代码包打包 RevoScaleR 和 revoscalepy，等。 绑定不会更改数据库引擎实例的支持模型，并且不会更改 SQL Server 的版本。

绑定是可逆的。 可以还原到 SQL Server 服务通过[取消绑定实例](#bkmk_Unbind)和修复 SQL Server 数据库引擎实例。

计算总和，绑定的步骤如下所示：

+ 使用现有的配置安装的 SQL Server 2016 R Services （或 SQL Server 2017 机器学习服务） 启动。
+ 确定哪个版本的 Microsoft 机器学习服务器具有你想要使用的已升级的组件。
+ 下载并运行该版本的安装程序。 安装程序检测到现有实例中，添加绑定选项，并返回兼容的实例的列表。
+ 选择你想要将绑定并在完成安装程序来执行绑定的实例。

在用户体验方面的技术和如何使用它保持不变。 唯一的区别是存在较新版本的包和最初可通过在 SQL Server （如 SQL Server 2016 R Services 的客户的 MicrosoftML) 的可能的其他包。

## <a name="bkmk_BindWizard"></a>将绑定到 MLS 使用安装程序

Microsoft 机器学习安装程序检测到的现有功能和 SQL Server 版本，并调用名为 SqlBindR.exe 若要更改绑定的实用工具。 在内部，SqlBindR 是链接到安装程序，间接使用。 更高版本，您可以直接从命令行执行特定的选项调用 SqlBindR。

1. 在 SSMS 中，运行`SELECT @@version`验证服务器是否满足最小的生成需求。 

   对于 SQL Server 2016 R Services，最小值是[Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)并[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。

1. 检查 R 基和 RevoScaleR 包以确认现有版本比你打算将其替换为较低的版本。 SQL Server 2016 R Services 的 R 基础包 3.2.2，RevoScaleR 8.0.3。

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

1. 关闭 SSMS 和无 SQL Server 的打开连接的任何其他工具。 绑定将覆盖程序文件。 如果 SQL Server 具有打开的会话，绑定将失败，绑定错误代码为 6。

1. 下载到具有你想要升级的实例的计算机上的 Microsoft Machine Learning Server。 我们建议[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解压缩文件夹，然后启动 ServerSetup.exe，MLSWIN93 下。

   ![Microsoft 机器学习服务器安装向导](media/mls-921-installer-start.PNG)

1. 上**配置安装**，确认要升级的组件，并查看兼容实例的列表。 

   此步骤非常重要。

   在左侧，选择想要保留还是升级每个功能。 无法升级某些功能而不是其他。 空的复选框中删除该功能，假定当前已安装。 屏幕截图中，给定的 SQL Server 2016 R Services (MSSQL13) 实例中选择 R 和预先训练的模型的 R 版本。 此配置是有效的因为 SQL Server 2016 支持 R 但不是 Python 支持。

   如果您正在升级 SQL Server 2016 R Services 上的组件，则选择 Python 功能。 不能将 Python 添加到 SQL Server 2016 R Services。

   在右侧，选择实例名称旁边的复选框。 如果未不列出任何实例，必须组合不兼容。 如果不选择实例，创建新的独立安装的机器学习服务器时，和 SQL Server 库保持不变。 如果您不能选择实例，它可能不是在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![配置安装步骤](media/mls-931-installer-mssql13.png)

1. 上**许可协议**页上，选择**我接受这些条款**的机器学习服务器接受许可条款。 

1. 在后续页上提供同意的选择，例如 Microsoft R Open 或 Python Anaconda 分发任何开放源代码组件的其他许可条件。

1. 上**几乎存在**页上，记下的安装文件夹。 默认文件夹是 \Program Files\Microsoft\ML 服务器。

    如果你想要更改安装文件夹，单击**高级**以返回到向导的第一页。 但是，你必须重复先前所做。

在安装过程中，替换为 SQL Server 使用的任何 R 或 Python 库和快速启动板更新为使用较新的组件。 因此，如果该实例之前使用默认 R_SERVICES 文件夹中的库，升级后删除这些库和快速启动板服务的属性更改为在新位置中使用的库。

绑定会影响这些文件夹的内容：C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 替换 C:\Program Files\Microsoft\ML Server\R_SERVER 的内容。 Microsoft 机器学习服务器安装程序创建第二个文件夹及其内容。 

如果升级失败，请[SqlBindR 错误代码](#sqlbindr-error-codes)有关详细信息。

## <a name="confirm-binding"></a>确认绑定

重新检查以确认你拥有较新版本的 R 和 RevoScaleR 的版本。 使用 R 控制台与你的数据库引擎实例中的 R 包分发获取包信息：

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

对于绑定到机器学习服务器 9.3 SQL Server 2016 R Services，R 基础包应 3.4.3、 RevoScaleR 应是 9.3，并且你还应 MicrosoftML 9.3。 

如果添加预先训练的模型，模型嵌入在 MicrosoftML 库，可以调用这些方法通过 MicrosoftML 函数。 有关详细信息，请参阅[MicrosoftML 的 R 示例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-binding-no-internet-access"></a>脱机绑定 （无 internet 访问权限）

对于未连接到 internet 的系统，可以安装程序和.cab 文件，下载到连接 internet 的计算机，然后将文件传输到独立服务器。 

安装程序 (ServerSetup.exe) 包括 Microsoft 包 （RevoScaleR、 MicrosoftML、 olapR、 sqlRUtils）。 .Cab 文件提供其他核心组件。 例如，"SRO"cab 提供了 R Open，Microsoft 的开放源代码 R 的分发

下面的说明解释如何将脱机安装的文件。

1. 下载 MLS 安装程序。 单个压缩文件的形式下载它。 我们建议[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但也可安装[早期版本](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下载的 cab 文件。 以下链接是 9.3 版。 如果需要早期版本，可以中找到更多链接[R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。 前面曾提到，Python/Anaconda 只能添加到 SQL Server 2017 机器学习服务实例。 预先训练的模型存在对 R 和 Python;.cab 文件提供了模型中使用的语言。

    | 功能 | 下载 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 预定型模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. .Zip 和.cab 文件传输到目标服务器。

1. 在服务器上，键入`%temp%`中运行命令来获取临时目录的物理位置。 物理路径因计算机而异，但它通常是`C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 将.cab 文件放在 %temp%文件夹中。

1. 解压缩安装程序。

1. 运行 ServerSetup.exe，并按照屏幕上的提示完成安装。

## <a name="bkmk_BindCmd"></a>命令行操作

在运行 Microsoft 机器学习服务器后，名为 SqlBindR.exe 的命令行实用工具将变为可用，您可将用于进一步绑定操作。 例如，如果您决定要反转一个绑定，您可以重新运行安装程序或使用命令行实用程序。 此外，可以使用此工具来检查实例兼容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 您可能还未运行安装程序。 SqlBindR 运行机器学习服务器安装程序之后仅将可用。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置是 C:\Program Files\Microsoft\MLServer\Setup

2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如，实例名称可能是 MSSQL14。对于默认实例，或服务器名类似的 MSSQLSERVER。MYNAMEDINSTANCE。

3. 运行**SqlBindR.exe**命令 */绑定*参数，并指定要升级的实例的名称使用上一步中返回的实例名称。

   例如，若要升级默认实例，请键入：  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 完成升级后，重新启动与已修改的任何实例关联的快速启动板服务。

## <a name="bkmk_Unbind"></a>还原或取消绑定实例

可以还原到初始安装的 R 和 Python 组件建立 SQL Server 安装程序的绑定的实例。 有三个部分恢复到 SQL Server 服务。

+ [步骤 1：从 Microsoft Machine Learning Server 取消绑定](#step-1-unbind)
+ [步骤 2：将实例还原到原始状态](#step-2-restore)
+ [步骤 3：重新安装任何添加到安装的包](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>第 1 步：取消绑定

有两个用于回滚绑定选项： 重新重新运行安装程序或使用 SqlBindR 命令行实用程序。

#### <a name="bkmk_wizunbind"></a> 取消绑定使用安装程序

1. 找到机器学习服务器的安装程序。 如果已删除安装程序，您可能需要再次下载它或将其复制从另一台计算机。
2. 请确保具有你想要取消绑定的实例的计算机上运行安装程序。
2. 安装程序会标识可作为取消绑定的对象的本地实例。
3. 取消选择你想要恢复到原始配置的实例旁边的复选框。
4. 接受许可协议。 安装时，你必须指示您接受许可条款甚至。
5. 单击 **“完成”**。 此过程需要一段时间。

#### <a name="bkmk_cmdunbind"></a> 取消绑定使用命令行

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如，以下命令恢复默认实例：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>第 2 步：修复 SQL Server 实例

运行 SQL Server 安装程序修复 R 和 Python 功能的数据库引擎实例。 会保留现有的更新，但如果你错过了任何 SQL Server 服务对 R 和 Python 包的更新，此步骤适用于这些修补程序。

或者，这是更多工作，但无法也完全卸载然后重新安装数据库引擎实例，并将所有服务更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步骤 3：添加任何第三方程序包

您可能添加了其他开放源代码或第三方包到包库。 反转绑定切换时的默认包库的位置，因为必须重新安装到的库，现在使用 R 和 Python 包。 有关详细信息，请参阅[默认包](installing-and-managing-r-packages.md)，[安装新 R 包](install-additional-r-packages-on-sql-server.md)，并[安装新的 Python 包](../python/install-additional-python-packages-on-sql-server.md)。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令语法

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

MLS 安装程序和 SqlBindR 这两个返回以下错误代码和消息。

|错误代码  | 消息           | 详细信息               |
|------------|-------------------|-----------------------|
|绑定错误 | 确定 （成功） | 无错误通过绑定。 |
|绑定错误 1 | 参数无效 | 语法错误。 |
|绑定错误 2 | 无效的操作 | 语法错误。 |
|绑定错误 3 | 无效的实例 | 实例存在，但不能用于绑定。 |
|绑定错误 4 | 没有可绑定 | |
|绑定错误 5 | 已绑定 | 已运行 *bind* 命令，但指定的实例已绑定。 |
|绑定错误 6 | 绑定失败 | 取消绑定实例时出错。 如果不选择任何功能运行 MLS 安装程序，可以发生此错误。 绑定要求选择 MSSQL 实例和 R 和 Python，认为实例是 SQL Server 2017。 如果 SqlBindR 无法写入 Program Files 文件夹，也会发生此错误。 打开的会话或 SQL Server 的句柄将导致出现此错误。 如果收到此错误，重新启动计算机并启动任何新会话之前的重做的绑定步骤。|
|绑定错误 7 | 未绑定 | 数据库引擎实例包含 R Services 或 SQL Server 机器学习服务。 实例未绑定到 Microsoft Machine Learning Server。 |
|绑定错误 8 | 取消绑定失败 | 取消绑定实例时出错。 |
|绑定错误 9 | 未找到任何实例 | 此计算机上未不找到任何数据库引擎实例。 |

## <a name="known-issues"></a>已知问题

本部分列出了已知的问题特定于使用 SqlBindR.exe 实用程序，或可能会影响 SQL Server 实例的机器学习服务器的升级。

### <a name="restoring-packages-that-were-previously-installed"></a>还原以前安装的包

如果您升级到 Microsoft R Server 9.0.1，该版本 SqlBindR.exe 的版本无法还原原始包或 R 组件完全，要求用户运行 SQL Server 修复的实例上，应用所有的服务版本，然后重新启动实例。

更高版本的 SqlBindR 自动还原原始的 R 功能，从而无需重新安装 R 组件，或重新修补服务器。 但是，必须安装在初始安装后可能已添加的任何 R 包更新。

如果已使用包管理角色来安装并共享包，此任务要容易得多： 可以使用 R 命令同步到文件系统在数据库中，使用记录已安装的包，反之亦然。 有关详细信息，请参阅[SQL Server 的 R 包管理](install-additional-r-packages-on-sql-server.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>从 SQL Server 的多个升级的问题

如果在运行 Microsoft R Server 9.1.0 的新安装程序时，你有以前升级到 9.0.1，SQL Server 2016 R Services 的实例，它显示的所有有效实例列表并则默认情况下会选择以前绑定的实例。 如果继续，以前绑定的实例是未绑定。 因此，早期 9.0.1 删除安装，包括任何相关的包，但未安装 Microsoft R Server (9.1.0) 的新版本。

解决此问题，您可以修改现有的 R Server 安装，如下所示：
1. 在控制面板中，打开**添加或删除程序**。
2. 找到 Microsoft R Server，并单击**更改/修改**。
3. 安装程序启动时，选择你想要将绑定到 9.1.0 的实例。

Microsoft Machine Learning Server 9.2.1 和 9.3，不具有此问题。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定会使多个临时文件夹

有时无法清理临时文件夹的绑定和取消绑定操作。
如果找到具有类似下面的名称的文件夹，可以在安装完成后删除它：R_SERVICES_<guid>

> [!NOTE]
> 请务必等待，直到安装已完成。 它可能需要很长时间才能删除与版本相关联的 R 库，然后添加新的 R 库。 操作完成后，会删除临时文件夹。

## <a name="see-also"></a>另请参阅

+ [安装机器学习服务器为 Windows (Internet 连接)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安装机器学习服务器为 Windows （脱机）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [机器学习服务器中的已知的问题](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [从以前的版本中的 R Server 的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已弃用，不再使用或更改的特性](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
