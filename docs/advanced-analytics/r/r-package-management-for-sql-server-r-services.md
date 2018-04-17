---
title: 安装和管理 SQL Server 中的机器学习包 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cbab4687dd0d5a8cb250fa38fc4c4c7dbb9d68a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="install-and-manage-machine-learning-packages-in-sql-server"></a>安装和管理 SQL Server 中的机器学习包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何安装新的 R 或 Python 包和 SQL Server 2016 中 SQL Server 自 2017 年。 它还描述你可以在 SQL Server 安装的包上的限制。

## <a name="overview-of-package-management-methods-and-requirements"></a>包管理方法和要求概述

与不同的是一个典型的 R 或 Python 开发，包使用的 SQL Server 必须安装到下的管理控制的文件夹。 有许多好处将包保存在单个位置：

+ 服务器管理员可以监视添加新文件和库的服务器上，并控制使用包库文件的增长。 
+ 包可以更方便地共享的多个数据库用户，而不是在用户库中安装的同一个包的多个副本。
+ 仅受保护、 已批准程序包可以进行安装，以保护服务器和其操作。

但是，这些限制一定数据科学家和分析师工作的方法中的某些更改：

+ 通常情况下，到服务器的管理访问权限是必需的。 在 SQL Server 自 2017 年，数据库管理员可以使用角色来使某些用户能够安装包用于是私有的但管理员仍必须启用此功能。
+ 许多服务器没有 Internet 访问权限。 程序包安装到这些计算机需要一些额外的准备工作。
+ 包将安装到实例库。 包无法在实例之间共享。
+ 用户无法运行任何用户库中已安装的包。

## <a name="package-installation-guides-for-r-or-python"></a>R 或 Python 的包安装指南

有关如何安装新的 R 或 Python 包，请参阅以下文章以了解详细步骤。 

### <a name="install-new-r-packages"></a>安装新的 R 包

+ [在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)

    作为管理员，使用 R 工具，你可以在 SQL Server 2016 或自 2017 年 1 上安装 R 包。

    你还可以从远程 R 客户端安装 R 包，R Server 9.0.2 或更高版本安装。

    你还可以在使用 DDL 语句的 SQL Server 2017 安装 R 包。

### <a name="install-new-python-packages"></a>安装新的 Python 软件包

+ [在 SQL Server 上安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>必要條件

在尝试下载或安装任何新包之前，查看的要求：

+ 请确保包的 Windows 版本：[获取正确的包版本和格式](#packageVersion)

+ 确定所有包依赖关系，并确定其与 SQL Server 环境的兼容性。

+ 验证 R 版本或 Python 版本兼容性。 此包必须与 R 或在 SQL Server 中运行的 Python 版本兼容。

+ 权限。 确定你是否具有权限才能安装包。 若要安装到实例库，运行 SQL Server 的计算机对管理访问权限是必需的。 如果你没有管理访问权限的 SQL Server 计算机，找到的数据库管理员联系，以帮助包安装。

    在 SQL Server 自 2017 年，你可以安装 R 包从远程客户端，如果管理包已在服务器上已启用，并且你是数据库所有者或包管理角色的成员。

+ 请考虑的风险和安装到 SQL Server 环境的特定包的优势。 检查是否包 （或它需要的任何包） 包含通过 SQL Server 或策略会阻止的功能。 很多 R 和 Python 包都可以强制写入的 SQL Server 环境很差适合。 问题可能包括：

    - 访问网络的包
    - 包，需要 Java 或 SQL Server 环境中通常不使用其他框架
    - 包，需要提升的文件系统访问权限
    - 包用于 web 开发或其他任务，不通过在 SQL Server 内部运行从中受益。

## <a name="installation-on-servers-with-no-internet-access"></a>在没有 Internet 访问权限的服务器上的安装

一般情况下，承载生产数据库的服务器不允许连接到 Internet。 在此类环境中安装新的 R 或 Python 包要求你事先准备的所有包和其依赖项，并将文件复制到在安装中使用的服务器上的文件夹。

1. 识别所有包依赖关系。 
2. 检查是否在服务器上已安装任何所需的程序包。 如果安装此包，请验证是否正确版本。
3. 将包和所有依赖项下载到单独的计算机。
4. 文件服务器移到可访问的文件夹。
5. 运行要将程序包安装到实例库的受支持的安装命令或 DDL 语句。

识别所有依赖项可能很复杂。 R、 中，我们建议你使用[miniCRAN](create-a-local-package-repository-using-minicran.md)准备一个脱机包存储库。

对于 Python，必须同样准备所有依赖项，然后将它们保存到本地。 请务必使用兼容 Windows 的二进制文件并使用 WHL 格式。
