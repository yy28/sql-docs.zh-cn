---
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553240"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

使用 Microsoft Connector for Oracle，可以从 SSIS 包内的 Oracle 数据源中导出数据，并向其中加载数据。

## <a name="version-support"></a>版本支持

Microsoft Connector for Oracle 支持以下 Microsoft SQL Server 产品：

- SQL Server 2019 及更高版本
- SQL Server Data Tools (SSDT)

支持以下 Oracle Database 版本的数据源：

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c（不支持 Windows 身份验证）

所有操作系统和平台都支持 Oracle Database。
> [!NOTE]
>
> 在 SQL Server 2019 中，Microsoft Connector for Oracle Database 不需要 Oracle 客户端。

## <a name="installation"></a>安装

如果需要在 SQL Server 中运行包，可以从[此处](https://www.microsoft.com/en-us/download/details.aspx?id=58228)获取 Microsoft Connector for Oracle Database 安装程序。 然后按照安装向导中的说明进行操作。

安装连接器后，必须重启 SQL Server Integration Services，才能确保 Oracle 源和目标正常运行。

如果需要使用连接器设计包，无需下载连接器。 自版本 15.9.0 起，SQL Server Data Tools (SSDT) 中随附它。

## <a name="uninstallation"></a>卸载

若要从 SQL Server 中删除 Microsoft Connector for Oracle Database，可以运行卸载向导。

## <a name="design-ssis-package-with-previous-version"></a>使用旧版本设计 SSIS 包

自版本 15.9.0 起，SSDT 已随附 Microsoft Connector for Oracle Database，因此在设计定目标到 SQL Server 2019 的 SSIS 包时，无需任何安装。

若要设计定目标到 SQL Server 2017 及更低版本的 SSIS 包，必须安装相应版本的适用于 Oracle 的 Attunity Connector。

**下载链接：**

- [SQL Server 2017：适用于 Oracle 的 Attunity Microsoft Connector 版本 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=55179)
- [SQL Server 2016：适用于 Oracle 的 Attunity Microsoft Connector 版本 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=52950)
- [SQL Server 2014：适用于 Oracle 的 Attunity Microsoft Connector 版本 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=44582)
- [SQL Server 2012：适用于 Oracle 的 Attunity Microsoft Connector 版本 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=29283)

## <a name="next-steps"></a>后续步骤

- 配置 [Oracle Connection Manager](oracle-connection-manager.md)。
- 配置 [Oracle 源](oracle-source.md)。
- 配置 [Oracle 目标](oracle-destination.md)。
- 若有任何疑问，请访问 [TechCommunity](https://aka.ms/AA5u35j)。
