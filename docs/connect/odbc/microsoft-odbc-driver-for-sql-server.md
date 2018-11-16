---
title: 适用于 SQL Server 的 Microsoft ODBC 驱动程序 | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a36070adf041363953ddaaf08675a2b9d649feb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603727"
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC 是适用于 SQL Server C 和 c + + 中编写的应用程序的主要本机数据访问 API。 没有大多数数据源的 ODBC 驱动程序。 可以使用 ODBC 的其他语言包括 COBOL、 Perl、 PHP 和 Python。 在数据集成方案中广泛使用 ODBC。

ODBC 驱动程序附带 [sqlcmd](../../tools/sqlcmd-utility.md) 和 [bcp](../../tools/bcp-utility.md) 等工具。 使用 sqlcmd 实用工具可以运行 Transact-SQL 语句、系统过程和 SQL 脚本。 bcp 实用工具可以在 Microsoft SQL Server 实例和用户指定格式的数据文件间大批量复制数据。 使用 bcp 实用工具可以将大量新行导入 SQL Server 表，或将表数据导出到数据文件。  

## <a name="code-example-in-c"></a>C + + 中的代码示例

下面的 c + + 示例演示如何使用 ODBC Api 连接到并访问数据库：

- [C + + 代码示例中，使用 ODBC](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>下载

- ![下载向下箭头线圈出](../../ssdt/media/download.png)[下载 ODBC 驱动程序](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>文档

### <a name="features"></a>功能

- [自定义密钥存储提供程序](../../connect/odbc/custom-keystore-providers.md)
- [DSN 和连接字符串关键字和属性](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) （提供的功能也适用，而无需 OLEDB、 SQL Server 的 ODBC 驱动程序）
- [使用 Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [使用 Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [使用透明网络 IP 解析](../../connect/odbc/using-transparent-network-ip-resolution.md)

### <a name="linux-and-macos"></a>Linux 和 macOS

- [安装驱动程序](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [连接到 SQL Server](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [使用 bcp 连接](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [使用 sqlcmd 进行连接](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [数据访问跟踪](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [常见问题解答](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [安装驱动程序管理器](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [已知问题](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [编程指南](../../connect/odbc/linux-mac/programming-guidelines.md)
- [发行说明](../../connect/odbc/linux-mac/release-notes.md)
- [支持高可用性和灾难恢复](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [使用集成身份验证 (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [异步执行（通知方法）示例](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Windows ODBC 驱动程序中的连接弹性](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [识别驱动程序的连接池](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [功能及行为变化](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [发行说明](../../connect/odbc/windows/release-notes.md)
- [系统要求、安装和驱动程序文件](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>社区  
- [Microsoft SQL Server ODBC 驱动程序团队博客](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server 数据访问论坛](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
