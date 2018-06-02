---
title: 在 SQL Server 计算机学习 Services 上安装新的 R 包 |Microsoft 文档
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services （数据库）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707075"
---
# <a name="install-new-r-packages-on-sql-server"></a>在 SQL Server 上安装新的 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何将新的 R 包安装到何处启用机器学习的 SQL Server 的实例。 有多种方法可以安装新的 R 包，具体取决于你拥有 SQL Server 的版本，以及服务器是否具有 internet 连接。 采用以下方法来新包安装是可能的。

| 方法                           | 权限               | 远程/本地 |
|------------------------------------|---------------------------|--------------|
| [使用传统的 R 包管理器](use-r-package-managers-on-sql-server.md)  | 管理员 | Local |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  启用管理的数据库角色之后 | both|
| [使用 T-SQL （创建外部库）](install-r-packages-tsql.md) | 启用管理的数据库角色之后 | both 

## <a name="who-installs-permissions"></a>用户安装 （权限）

R 包库物理上位于您的 SQL Server 实例，具有受限访问权限的安全文件夹中的 Program Files 文件夹。 写入到此位置需要管理员权限。

非管理员才能安装包，但这样做需要 addititional 配置和功能在初始安装中不可用。 对于非管理员包安装两种方法： RevoScaleR 使用 9.0.1 版和更高版本，或使用创建外部库 (仅 2017 SQL Server)。 在 SQL Server 2017 **dbo_owner**或具有创建外部库权限的另一个用户可以将 R 包安装到当前数据库。

R 开发人员都习惯于创建它们需要位于中心位置的库是否 off-limits 的包的用户库。 这种做法是为 SQL Server 数据库引擎实例中执行的 R 代码有问题。 SQL Server 无法从外部库加载包，即使该库位于同一台计算机上。 在 SQL Server 中运行的 R 代码中，可以使用仅实例库中的包。

文件系统访问通常被限制在服务器上，且在 SQL Server 中执行外部脚本运行时即使到服务器上的用户文档文件夹具有管理员权限和访问权限，无法访问安装默认实例之外的任何包库。 

## <a name="considerations-for-package-installation"></a>包安装注意事项

在安装新包之前, 请考虑由给定包启用的功能是否适合在 SQL Server 环境中。 上一个强制写入的 SQL Server 环境，你可能想要避免以下环境：

+ 需要网络访问的包
+ 包，需要 Java 或 SQL Server 环境中通常不使用其他框架
+ 包，需要提升的文件系统访问权限
+ 包用于 web 开发或不，通过在 SQL Server 内部运行从中受益的其他任务

## <a name="offline-installation-no-internet-access"></a>脱机安装 （无 internet 访问权限）

一般情况下，承载生产数据库的服务器阻止 internet 连接。 在此类环境中安装新的 R 或 Python 包要求你事先准备包和依赖项，并将文件复制到脱机安装服务器上的文件夹。

识别所有依赖项会变得复杂。 R、 中，我们建议你使用[miniCRAN 创建本地存储库](create-a-local-package-repository-using-minicran.md)，然后将完全定义的存储库传输到独立的 SQL Server 实例。

Alternativley，可以手动执行此步骤：

1. 识别所有包依赖关系。 
2. 检查是否在服务器上已安装任何所需的程序包。 如果安装此包，请验证是否正确版本。
3. 将包和所有依赖项下载到单独的计算机。
4. 文件服务器移到可访问的文件夹。
5. 运行要将程序包安装到实例库的受支持的安装命令或 DDL 语句。

### <a name="download-the-package-as-a-zipped-file"></a>下载包为压缩文件

如果没有 internet 连接的服务器上的安装，必须下载脱机安装的压缩文件的格式中的包的副本。 **请不要解压缩包。**

例如，下面的过程描述现在，若要获取的正确版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) bioconductor，假定计算机具有 internet 访问权限的包。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击的链接。ZIP 文件，并选择**目标另存为**。

3.  导航到本地文件夹，zip 的包存储中，然后单击**保存**。

    此过程将创建包的本地副本。 

4. 如果你收到下载错误，请尝试不同的镜像站点。

5. 已下载包存档后，你可以安装包，或将压缩的包复制到没有 internet 访问的服务器。

> [!TIP]
> 如果错误地安装而不是下载二进制文件的包，下载的压缩文件的副本还会保存到你的计算机。 为包已安装，以确定文件位置，请观看的状态消息。 可以将该 zip 的文件复制到没有 internet 访问的服务器。
> 
> 但是，当你获得包使用此方法时，将不包括依赖关系。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>与独立 R 或 Python 服务器通过并行安装

R 和 Python 功能包括在多个 Microsoft 产品，它们都无法共存于同一台计算机。

如果你安装 SQL Server 自 2017 年 1 Microsoft 机器学习 Server （独立） 或 SQL Server 2016 R Server （独立） 除了数据库中分析 （SQL Server 自 2017 年 1 机器学习服务和 SQL Server 2016 R Services），你的计算机拥有单独对于每个，包含重复项的所有 R 工具和库的 R 安装。

这些包安装到 R_SERVER 库只由独立服务器，并且不由 SQL Server （数据库） 实例访问。 始终使用`R_SERVICES`库安装你想要使用 SQL Server 上的数据库中的包时。 有关路径的详细信息，请参阅[包库位置](installing-and-managing-r-packages.md#package-library-location)。


## <a name="see-also"></a>另请参阅

+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)