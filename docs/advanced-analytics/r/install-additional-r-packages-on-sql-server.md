---
title: 安装新的 R 语言包
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 机器学习服务 (数据库内)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1048dc6ef0a43c5fa41dd5398a5b3dced4a5ebe8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715107"
---
# <a name="install-new-r-packages-on-sql-server"></a>在 SQL Server 上安装新的 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何将新的 R 包安装到启用机器学习的 SQL Server 实例中。 有多种方法可用于安装新的 R 包, 具体取决于 SQL Server 的版本以及服务器是否具有 internet 连接。 可以通过以下方法来安装新的包。

| 方法                           | 权限               | 远程/本地 |
|------------------------------------|---------------------------|--------------|
| [使用传统的 R 包管理器](use-r-package-managers-on-sql-server.md)  | 管理员 | Local |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  此后启用了管理员的数据库角色 | both|
| [使用 T-sql (CREATE EXTERNAL LIBRARY)](install-r-packages-tsql.md) | 此后启用了管理员的数据库角色 | both 

## <a name="who-installs-permissions"></a>谁安装 (权限)

R 包库以物理方式位于 SQL Server 实例的 Program Files 文件夹中, 位于具有受限访问权限的安全文件夹中。 写入此位置需要管理员权限。

非管理员可以安装包, 但这样做需要在初始安装时不提供额外的配置和功能。 非管理包安装有两种方法:使用9.0.1 和更高版本的 RevoScaleR, 或使用 CREATE EXTERNAL LIBRARY (仅 SQL Server 2017)。 在 SQL Server 2017 中, **dbo_owner**或具有 CREATE EXTERNAL LIBRARY 权限的其他用户可以将 R 包安装到当前数据库。

如果集中定位的库是不受限制的, 则 R 开发人员习惯于为所需的包创建用户库。 此做法在 SQL Server 数据库引擎实例中执行 R 代码时出现问题。 SQL Server 无法从外部库加载包, 即使该库位于同一台计算机上也是如此。 只有实例库中的包可用于在 SQL Server 中运行的 R 代码。

文件系统访问通常在服务器上受到限制, 即使您对服务器上的用户文档文件夹具有管理员权限和访问权限, 在 SQL Server 中执行的外部脚本运行时仍无法访问在默认实例之外安装的任何包类库. 

## <a name="considerations-for-package-installation"></a>包安装注意事项

在安装新包之前, 请考虑给定包启用的功能是否适用于 SQL Server 环境。 在强化的 SQL Server 环境中, 你可能需要避免以下情况:

+ 需要网络访问的包
+ 需要提升文件系统访问权限的包
+ 包用于 web 开发或其他无法通过在中运行的任务 SQL Server

## <a name="offline-installation-no-internet-access"></a>脱机安装 (无 internet 访问)

通常, 托管生产数据库的服务器会阻止 internet 连接。 在此类环境中安装新的 R 或 Python 包需要提前准备包和依赖项, 并将文件复制到服务器上的某个文件夹以进行脱机安装。

标识所有依赖项都非常复杂。 对于 R, 建议使用[miniCRAN 创建本地存储库](create-a-local-package-repository-using-minicran.md), 然后将完全定义的存储库传输到隔离的 SQL Server 实例。

或者, 你可以手动执行以下步骤:

1. 标识所有包依赖关系。 
2. 检查服务器上是否已安装了任何所需的包。 如果安装了包, 请验证版本是否正确。
3. 将包和所有依赖项下载到不同的计算机。
4. 将文件移动到服务器可以访问的文件夹。
5. 运行受支持的安装命令或 DDL 语句, 将包安装到实例库。

### <a name="download-the-package-as-a-zipped-file"></a>将包下载为压缩文件

若要在没有 internet 访问权限的情况下在服务器上安装, 必须以压缩文件格式下载包的副本, 以便进行脱机安装。 **不要将包解压缩。**

例如, 下面的过程介绍了如何从 Bioconductor 获取[FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)包的正确版本, 前提是计算机有权访问 internet。

1.  在“包存档”列表中，查找“Windows 二进制文件”版本。

2.  右键单击指向的链接。ZIP 文件, 然后选择 "**将目标另存为**"。

3.  导航到存储 zip 包的本地文件夹, 然后单击 "**保存**"。

    此过程将创建包的本地副本。 

4. 如果收到下载错误, 请尝试其他镜像站点。

5. 下载包存档后, 可以安装包, 或将压缩的包复制到无法访问 internet 的服务器。

> [!TIP]
> 如果在安装包时出错, 而不是下载二进制文件, 则会将下载的压缩文件的副本保存到计算机。 查看状态消息, 因为安装了包来确定文件位置。 可以将该压缩文件复制到无法访问 internet 的服务器。
> 
> 但是, 在使用此方法获取包时, 不会包含依赖项。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>与独立 R 或 Python 服务器并行安装

R 和 Python 功能包含在多个 Microsoft 产品中, 它们都可以共存于同一台计算机上。

如果安装了 SQL Server 2017 Microsoft Machine Learning Server (独立版) 或 SQL Server 2016 R Server (独立版), 则除了数据库内分析 (SQL Server 机器学习服务和 SQL Server 2016 R Services) 以外, 计算机的为每个安装 R, 其中包含所有 R 工具和库的重复项。

安装到 R_SERVER 库的包仅供独立服务器使用, 不能由 SQL Server (数据库内) 实例访问。 安装要在`R_SERVICES` SQL Server 中使用的数据库的包时, 请始终使用库。 有关路径的详细信息, 请参阅[包库位置](../package-management/default-packages.md)。

## <a name="see-also"></a>请参阅

+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)
