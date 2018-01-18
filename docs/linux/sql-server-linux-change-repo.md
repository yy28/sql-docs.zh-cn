---
title: "在 Linux 上的 SQL Server 的注册正式版存储库 |Microsoft 文档"
description: "从预览版 SQL Server 2017 存储库的存储库更改到正式版 (GA) 存储库在 Linux 上 （GA 有时也称为 RTM）。"
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: f74c74bddf8337bf4555ce4ecdf0b6e2c869e44f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>从预览版存储库的存储库更改到 GA 存储库

从 CTP 2.1、 RC1 或 RC2 的 SQL Server 2017 升级到正式版 (GA) 推出时您必须切换存储库。 以下部分说明你选择的存储库以及如何使在升级之前的更改。

## <a name="repository-choices"></a>存储库选项

请务必请注意，有两种主要类型的每个分布的存储库：

  > [!IMPORTANT]
  > 在升级到正式版之前，必须将任何 CTP 2.1 之前的版本升级到至少 2.1

- **累积更新 (CU)**: 累积更新 (CU) 存储库包含自该版本为基的 SQL Server 版本和任何 bug 修复或改进的包。 累积更新是特定于发行版中，如 SQL Server 自 2017 年。 正则的频率发布它们。

- **GDR**: GDR 储存库自该版本中包含的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步 CU 发行版。

每个 CU 和 GDR 版本包含完整的 SQL Server 程序包和所有以前的更新，该存储库。 从 GDR 版本更新到 CU 版本受更改 SQL Server 配置的存储库。 你还可以[降级](sql-server-linux-setup.md#rollback)到在主要版本中的任何版本 (ex： 自 2017 年)。

> [!NOTE]
> 你可以从 GDR 版本更新到 CU 释放任何时候通过更改存储库。 更新从 CU 的 GDR 发行版的版本不支持。 

## <a name="change-to-a-ga-repository"></a>更改到 GA 存储库

若要从预览存储库将更改为一个源代码存储库 （CU 或 GDR），使用以下步骤：

1. 删除以前配置的预览存储库。

   | 平台 | 存储库删除命令 |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. 有关**Ubuntu 仅**，导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 配置新的存储库。

   | 平台 | 存储库 | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [安装](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)使用 GA 存储库的 SQL Server。

   > [!IMPORTANT]
   > 此时，如果你选择执行完全安装使用[快速入门教程](#platforms)，请记住您刚配置的目标存储库。 不在本教程中重复该步骤。 这是如果你配置 GDR 存储库，尤其如此，因为快速入门教程使用 CU 存储库。

## <a name="next-steps"></a>后续步骤

有关如何在 Linux 上安装 SQL Server 自 2017 年的详细信息，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md)。
