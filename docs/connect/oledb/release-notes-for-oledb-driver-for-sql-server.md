---
title: 发行说明（适用于 SQL Server 的 OLE DB 驱动程序）| Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161764"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server 发行说明

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

本页介绍 Microsoft OLE DB 驱动程序的每个版本中添加适用于 SQL Server。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

2019 年 2 月

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 支持 utf-8 服务器编码。 | &bull; &nbsp; [OLE DB Driver for SQL Server 中的 UTF-8 支持](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 身份验证支持。 | &bull; &nbsp; [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018 年 7 月

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 为支持`UseFMTONLY`连接字符串关键字和`SSPROP_INIT_USEFMTONLY`初始化属性。 | `UseFMTONLY` 控制元数据的检索方式连接到时[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本。<br/><br/>&bull; &nbsp; [结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>修复的 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 修改后的 BCP 格式文件的正确版本。 | OLE DB 驱动程序 18.0 错误地将 18.0，BCP 格式化文件的版本而不是设置为 11.0。<br/><br/>不能通过 OLE DB 驱动程序 18.1 读取生成的 OLE DB 驱动程序 18.0 的格式文件。<br/><br/>如果您需要使用生成的驱动程序和新的驱动程序的以前版本的格式文件，可以手动编辑文件以将版本更改为 11.0。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 为支持`MultiSubnetFailover`连接字符串关键字和`SSPROP_INIT_MULTISUBNETFAILOVER`初始化属性。 | &bull; &nbsp; [OLE DB Driver for SQL Server 支持高可用性和灾难恢复](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。<br/><br/>&bull; &nbsp; [结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另请参阅

[适用于 SQL Server 的 Microsoft OLE DB 驱动程序](oledb-driver-for-sql-server.md)
