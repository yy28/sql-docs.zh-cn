---
title: 什么是 SQL Server 计算机学习 Services？ | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ecd58ee9670724a2732ce8aabc5d9f2c62042995
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585449"
---
# <a name="what-is-sql-server-machine-learning-services"></a>什么是 SQL Server 计算机学习 Services？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 计算机学习 Services 是嵌入、 预测分析和数据科学引擎，可以执行 SQL Server 数据库中的 R 和 Python 代码，作为存储过程、 T-SQL 脚本包含 R 或 Python 的语句，或作为 R 或 Python 包含的代码T-SQL。 

机器学习服务的关键价值主张是其专有包功能来提供在缩放，以及将计算和对数据所在的位置处理的功能的高级的分析消除跨请求数据的需要网络。

有为使用 SQL Server 中的机器学习功能的两个选项： 

+ [**SQL Server 计算机学习 Services （数据库）** ](r/sql-server-r-services.md)的范围内计算引擎，完全集成与数据库引擎的数据库引擎实例操作。 大多数安装是此选项。
+ [**SQL Server 计算机学习服务器 （独立）** ](r/r-server-standalone.md)是机器学习用于 Windows 的服务器运行独立于数据库引擎。 尽管你使用 SQL Server 安装程序以安装服务器，不是识别实例的功能。 就功能而言，它等效于非 SQL Server [Microsoft 机器学习用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

## <a name="r-and-python-packages"></a>R 和 Python 包

对每种语言的支持是通过用于创建和定型模型为各种类型，评分的数据，并且使用的基础系统资源的并行处理的专有 Microsoft 软件包。

由于专有包基于开放源代码 R 和 Python 分发版，因此脚本或在 SQL Server 中运行的代码也可以调用基函数并使用与 SQL Server 中提供的语言版本兼容的第三方包 (Python 3.5 和最新版本的 R，当前 3.3.3）。

| R  | Python | Description |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | 在这些库中的函数包括最广泛使用。 在这些库中找到数据转换和操作、 统计摘要、 可视化和建模和分析数据的多个窗体。 此外，在这些库中的函数会自动将工作负荷分散到可用的内核数，以便执行并行处理，处理所协调和管理计算引擎的数据块的能力。 |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 行业领先的机器学习算法映像特征化、 分类问题，和的详细信息。 |
| [olapR](r/how-to-create-mdx-queries-using-olapr.md) | none | 生成或在 R 脚本中执行 MDX 查询。
| [sqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | none | 函数将 R 脚本放入 T-SQL 的存储过程，与数据库中注册的存储的过程和 R 开发环境中运行存储的过程。
| [mrsdeploy](operationalization-with-mrsdeploy.md) | none | 主要用于在非 SQL 安装中的机器学习服务器，如[（独立版） 版本](r/r-server-standalone.md)。 此包用于部署和承载 web 服务、 生成与专用 web 的横向扩展拓扑和计算节点、 本地和远程会话，运行诊断和的详细信息之间切换。 对于 （数据库中） 安装，使用此包中的客户端容量： 例如，若要访问远程服务器上的 web 服务专用于运行仅机器学习服务工作负荷。 |

通过包分发和内置于多个产品的解释程序发送的自定义 R 和 Python 代码可移植性。 SQL Server 中提供了同一个包也会出现在多个其他 Microsoft 产品和服务，包括一个名为的非 SQL 版本[Microsoft 机器学习 Server](https://docs.microsoft.com/machine-learning-server/)。 可用的客户端，包括我们 R 和 Python 解释程序包括[Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)和[Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

包和解释程序也是可用的多[Azure 虚拟机](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)，Azure 机器学习和 Azure 服务，如[HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight)。 


## <a name="use-cases"></a>用例

**数据库中分析**

开发人员和分析师通常具有本地的 SQL Server 实例上运行的代码。 如果你具有 SQL Server 和一个 IDE 如[Visual Studio 与 R](https://docs.microsoft.com/visualstudio/rtvs/)或[Visual Studio 和 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)的同一计算机上，你可以生成、 训练和在其中任一种语言中本地测试模型。 本地访问简化了管理包： 作为管理员，你可以加载该角色使用内置权限的其他第三方包。

数据库中分析的最常见方法是使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)运行 R 或 Python 脚本。 中列出的教程[下一步行动](#next-steps)将帮助你入门。

**客户端-服务器配置**

从任何具有一个 IDE 的客户端工作站安装[Microsoft R 客户端](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)或[Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)，，然后编写推送执行的代码 (称为*远程计算上下文*)对数据和与远程 SQL 服务器的操作。 

同样，如果你使用的开发人员版，你可以生成使用相同的库和解释程序，客户端工作站上的解决方案中，并随后部署 SQL Server 机学习服务 （数据库） 上的生产代码。 

## <a name="version-history"></a>版本历史记录

SQL Server 自 2017 年 1 机器学习 Services 是 SQL Server 2016 R Services，增强，具有 Python 的下一代。 下表是所有版本中，从开始到当前版本的完整列表。 

| 产品名称 | 引擎版本 | 发布日期 |
|--------------|---------|--------------|
| SQL Server 自 2017 年 1 机器学习服务 （数据库） | R Server 9.2.1 <br/> Python 服务器 9.2 | 2017 年 10 月 |
| SQL Server 自 2017 年 1 机器学习服务器 （独立） | R Server 9.2.1 <br/> Python 服务器 9.2 | 2017 年 10 月 |
| SQL Server 2016 R Services （数据库） | R Server 9.1  | 自 2017 年 7 月  |
| SQL Server 2016 R Server （独立）  |  R Server 9.1 | 自 2017 年 7 月 |



## <a name="documentation-for-each-version"></a>每个版本的文档

SQL Server 文档的最新版本的版本不可知。 对于 SQL Server 机器学习服务，Python 才可用 2017年及更高版本，在所有版本中 R 支持时。 除非另外说明，你可以假定 R 文档适用于 2016年和 2017年版本。


## <a name="related-machine-learning-products"></a>相关的机器学习产品

 +  [设置 Azure 虚拟机](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure 应用商店包括包括计算机学习 Server 或 R Server 的多个虚拟机映像。 在 Microsoft Azure 中创建虚拟机是最快的方法，以获取对开发和部署预测模型。 映像附带的缩放和共享已配置，这样，就更容易将应用程序内的分析，并与后端系统集成的功能。

+ [数据科学虚拟机](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  数据科学虚拟机的最新版本包括计算机学习 Server，SQL Server，加上的机器学习，最常用的工具数组所有预安装和测试。 创建 Jupyter 笔记本、 Julia 中开发解决方案和使用 MXNet、 CNTK，等 TensorFlow GPU 启用深入学习库。

<a name="next-steps"></a>

## <a name="next-steps"></a>后续步骤

**步骤 1:** 安装和配置软件。 

+ [安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](install/sql-machine-learning-services-windows-install.md)

**步骤 2:** 开始使用代码中使用的以下教程之一：

+ [教程： 在 T-SQL 中运行 Python](tutorials/run-python-using-t-sql.md)
+ [教程： 在 T-SQL 中运行 R](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**步骤 3:** 添加你最喜欢的 R 和 Python 程序包并将它们与由 Microsoft 提供的包配合使用

+ [SQL Server 的 R 包管理](r/install-additional-r-packages-on-sql-server.md)
