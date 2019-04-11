---
title: 适用于 Windows 上 SQL Server 的 ODBC 的发行说明 | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-jizho2, v-chojas, genemi
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: f74d5a70325fdceb311bb3a45ba6824e64242ff0
ms.sourcegitcommit: 1a4aa8d2bdebeb3be911406fc19dfb6085d30b04
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58872007"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>适用于 Windows 上 SQL Server 的 ODBC 的发行说明

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本发行说明文章介绍适用于 Windows 上 SQL Server 的 Microsoft ODBC 驱动程序的新增功能。

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="173-february-2019"></a>17.3 版，2019 年 2 月

| 新增功能 | 详细信息 |
| :------------ | :------ |
| Azure Active Directory 托管服务标识（系统和用户分配）身份验证模式。 | 请参阅[结合使用 Azure Active Directory 和 ODBC Driver](../using-azure-active-directory.md)。 |
| 能够针对 Always Encrypted 列流式传输输入参数。 | 请参阅[使用 Always Encrypted 时的 ODBC 驱动程序限制](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)。 |
| XA 分布式事务。 | [使用 XA 事务](../use-xa-with-dtc.md)。 |
| bug 修复。 | 请参阅 [bug 修复](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2 版，2018 年 7 月

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 Azure SQL 数据库和 SQL Server 进行数据分类。 | 请参阅[数据分类](../data-classification.md)。 |
| 支持 UTF-8 服务器编码。 | &nbsp; |
| bug 修复。 | 请参阅 [bug 修复](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1 版，2018 年 3 月

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 支持 `SQL_COPT_SS_CEKCACHETTL` 和 `SQL_COPT_SS_TRUSTEDCMKPATHS` 连接属性。 | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>允许控制列加密密钥的本地缓存的保留时间以及刷新该时间。<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>允许应用程序将 AE 操作限制为仅使用指定的列主密钥列表。<br/><br/> 有关详细信息，请参阅[在 ODBC Driver for SQL Server 中使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| Azure Active Directory 交互式身份验证支持 | &nbsp; |
| bug 修复。 | 请参阅 [bug 修复](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17 版，2018 年 2 月

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 BCP API 的 Always Encrypted 支持。 | &nbsp; |
| 新连接字符串属性 `UseFMTOnly`。 | 使驱动程序在需要临时表的特殊情况下使用旧的元数据。 |
| 支持 Azure SQL 托管实例。 | 扩展的个人预览版。<br/><br/>请参阅下面的[使用托管实例（ODBC 版本 17）时的差异](#diffs-managed-instance-17)列表。 |
| &nbsp; | &nbsp; |

| 更改的依赖项 | 详细信息 |
| :------------ | :------ |
| 删除了 Microsoft 联机服务登录助手 | 该依赖项已删除。 |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> 使用托管实例（ODBC 版本 17）时的差异

此版本的 ODBC 包含对 Azure SQL 托管实例（扩展的个人预览版）的支持。 请参阅如下列出的使用托管实例时的差异列表。

> [!NOTE]
> 使用托管实例时存在许多差异：
>
> - 不支持 FILESTREAM。
> - 不支持本地文件系统访问，但这对于跟踪文件等类似内容是必需的。
> - 不支持从本地路径创建 UDT。
> - 不支持 Windows 集成身份验证。
> - 不支持 DTC。
> - `sa` 帐户不存在（默认帐户称为 `cloudSA`）。
> - TDS 令牌错误 (0xAA) 返回不正确的服务器名称。
> - 不支持数据库名称中的特殊字符。
> - 不支持 ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]。
> - 无论语言设置如何，错误消息始终以英语显示（与 Azure 相同）。

## <a name="131"></a>13.1

| 新增功能 | 详细信息 |
| :------------ | :------ |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 添加了对 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 和 [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) 的支持。 | 连接到 Microsoft SQL Server 2016 或更高版本时即可使用这些新增支持。 |
| 存在与对 Always Encrypted 和 Azure Active Directory 的支持相对应的连接池关键字和属性。 | [ODBC Driver for SQL Server 中识别驱动程序的连接池](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)中介绍了这些关键字和属性。 |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 添加对 Microsoft SQL Server 2016 的支持。 | 保留 ODBC 驱动程序版本 11 的功能。 |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 包含新功能。 | 请参阅 [Windows 上 Microsoft ODBC Driver for SQL Server 的功能](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)。 |
| 包含 SQL Server 2012 Native Client 中 ODBC 附带的所有功能。 | &nbsp; |
| &nbsp; | &nbsp; |
