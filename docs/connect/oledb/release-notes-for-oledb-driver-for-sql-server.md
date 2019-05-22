---
title: 发行说明（适用于 SQL Server 的 OLE DB 驱动程序）| Microsoft Docs
ms.date: 05/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 969caa46506c9fd19410c5ace753076b3ba02fbe
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65619988"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 Microsoft OLE DB 驱动程序发行说明

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

本页讨论添加到适用于 SQL Server 的 Microsoft OLE DB 驱动程序的每个版本中的内容。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1822"></a>18.2.2

2019 年 5 月

### <a name="bugs-fixed"></a>已修复 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 已修复多线程单元 (MTA) 中的非交互式 Azure Active Directory 身份验证。 | OLE DB 驱动程序 18.2.1 错误地尝试更改之前初始化为多线程的单元 (MTA) 上的 COM 并发模型。 因此，在调用 [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522) 接口前，在对 [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) 或 [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) 发出一个以上的后续调用的应用程序中，使用任何 Azure Active Directory 身份验证模式时，该驱动程序都会连接失败。 |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

2019 年 2 月

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 支持 UTF-8 服务器编码。 | &bull; &nbsp; [OLE DB Driver for SQL Server 中的 UTF-8 支持](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 身份验证支持。 | &bull; &nbsp; [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018 年 7 月

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 `UseFMTONLY` 连接字符串密钥以及 `SSPROP_INIT_USEFMTONLY` 初始化属性的支持。 | 连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本时，`UseFMTONLY` 会控制检索元数据的方式。<br/><br/>&bull; &nbsp; [结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>已修复 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 已修复 BCP 格式化文件的错误版本。 | OLE DB 驱动程序 18.0 错误地将 BCP 格式化文件的版本设为 18.0，而不是 11.0。<br/><br/>OLE DB 驱动程序 18.0 生成的格式文件无法由 OLE DB 驱动程序 18.1 读取。<br/><br/>如果需要通过新的驱动程序使用以前版本的驱动程序生成的格式文件，则可以手动编辑文件以将版本更改为 11.0。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 `MultiSubnetFailover` 连接字符串密钥以及 `SSPROP_INIT_MULTISUBNETFAILOVER` 初始化属性的支持。 | &bull; &nbsp; [OLE DB Driver for SQL Server 支持高可用性和灾难恢复](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。<br/><br/>&bull; &nbsp; [结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另请参阅

[适用于 SQL Server 的 Microsoft OLE DB 驱动程序](oledb-driver-for-sql-server.md)
