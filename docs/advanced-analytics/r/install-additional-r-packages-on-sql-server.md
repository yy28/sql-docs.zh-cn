---
title: 安装新的 R 语言包-SQL Server 机器学习服务
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务 （数据库内）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f443113222181f0909bd72048e3c3f5c739df4ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506928"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server 上安装新的 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何将新的 R 包安装到其中启用机器学习的 SQL Server 实例。 有多种方法来安装新的 R 包，具体取决于你拥有的 SQL Server 的版本，以及服务器是否具有 internet 连接。 可使用以下方法来安装新包。

| 方法                           | 权限               | 远程/本地 |
|------------------------------------|---------------------------|--------------|
| [使用传统的 R 包管理器](use-r-package-managers-on-sql-server.md)  | 管理员 | Local |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  之后管理员启用数据库角色 | both|
| [使用 T-SQL （创建外部库）](install-r-packages-tsql.md) | 之后管理员启用数据库角色 | both 

## <a name="who-installs-permissions"></a>用户安装 （权限）

R 包库物理上位于您的 SQL Server 实例，在具有受限访问权限的安全文件夹中的 Program Files 文件夹。 写入到此位置需要管理员权限。

非管理员可以安装包，但执行此操作需要 addititional 配置和功能在初始安装中不可用。 有两种方法对于非管理员包安装：RevoScaleR 使用 9.0.1 版和更高版本，或使用 CREATE EXTERNAL LIBRARY (仅 SQL Server 2017)。 在 SQL Server 2017 **dbo_owner**或具有 CREATE EXTERNAL LIBRARY 权限的另一个用户可以将 R 包安装到当前数据库。

R 开发人员习惯于创建所需位于中心位置的库是否仍受限的包的用户库。 这种做法是为 SQL Server 数据库引擎实例中执行 R 代码有问题。 SQL Server 无法从外部库加载包，即使该库是同一台计算机上。 SQL Server 中运行 R 代码中，可以使用仅实例库中的包。

通常在服务器上限制文件系统访问，即使到服务器上的用户文档文件夹具有管理员权限和访问，在 SQL Server 中执行的外部脚本运行时无法访问安装默认实例之外的任何包库。 

## <a name="considerations-for-package-installation"></a>包安装注意事项

然后再安装新的包，请考虑是否适合在 SQL Server 环境中由给定包启用的功能。 在强化的 SQL Server 环境中，你可能想要避免以下：

+ 需要网络访问权限的包
+ 需要 Java 或 SQL Server 环境中通常不使用其他框架的包
+ 需要提升权限的文件系统访问权限的包
+ 包用于 web 开发或通过在 SQL Server 内运行并不受益的其他任务

## <a name="offline-installation-no-internet-access"></a>脱机安装 （无 internet 访问权限）

一般情况下，承载生产数据库的服务器阻止 internet 连接。 在此类环境中安装新的 R 或 Python 包将要求您提前准备包和依赖项并将文件复制到用于脱机安装的服务器上的文件夹。

识别所有依赖项变得复杂。 对于 R，我们建议你使用[miniCRAN 创建本地存储库](create-a-local-package-repository-using-minicran.md)然后将完全定义的存储库传输到独立的 SQL Server 实例。

Alternativley，可以手动执行此步骤：

1. 识别所有包依赖项。 
2. 检查是否在服务器上已安装任何所需的包。 如果安装此包，请验证版本是否正确。
3. 将包和所有依赖项下载到单独的计算机。
4. 服务器将文件移动到可以访问的文件夹。
5. 运行受支持的安装命令或 DDL 语句以将包安装到实例库。

### <a name="download-the-package-as-a-zipped-file"></a>压缩文件以下载包

对于无法访问 internet 的服务器上安装，必须下载脱机安装一个压缩文件的格式中的包的副本。 **请不要解压缩包。**

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)请假设该计算机有权访问 internet 的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，然后选择**目标另存为**。

3.  导航到本地文件夹 zip 的包存储中，然后单击**保存**。

    此过程将创建包的本地副本。 

4. 如果遇到下载错误，请尝试不同的镜像站点。

5. 下载包存档后，可以安装包，或将压缩的包复制到不具有 internet 访问的服务器。

> [!TIP]
> 如果错误地安装而无需下载二进制文件的包，下载压缩文件的副本也会保存到您的计算机。 观看安装此包以确定文件位置的状态消息。 可以将该压缩的文件复制到不具有 internet 访问的服务器。
> 
> 但是，当您获得使用此方法的包时，将不包括依赖项。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>通过并行安装与独立 R 或 Python 服务器

R 和 Python 功能包括在多个 Microsoft 产品，所有这些无法同时存在同一台计算机。

如果除了数据库内分析 （SQL Server 2017 机器学习服务和 SQL Server 2016 R Services） 中安装 SQL Server 2017 Microsoft Machine Learning Server （独立版） 或 SQL Server 2016 R Server （独立版），您的计算机具有单独每个重复项的所有 R 的工具和库使用 R 的的安装。

安装到 r_server LIBRARY 库的包仅由独立服务器和 SQL Server （数据库内） 实例无法访问。 始终使用`R_SERVICES`库安装你想要使用 SQL Server 上数据库中的包时。 有关路径的详细信息，请参阅[包库位置](installing-and-managing-r-packages.md#package-library-location)。


## <a name="see-also"></a>另请参阅

+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)