---
title: 连接库和框架 |Microsoft Docs
description: 列出了客户端应用程序可用于从各种语言连接到 Microsoft SQL Server 运行在本地或云中、 在 Linux、 Windows 或 Docker 上以及到 Azure SQL 数据库和 Azure SQL 数据仓库连接驱动程序。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: 37b6714a11adc9a64b796830183ecc02101a4823
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394628"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>适用于 Microsoft SQL Server 的连接库和框架

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

请查看[入门教程](http://aka.ms/sqldev)来快速开始使用 C#、 Java、 Node.js、 PHP 和 Python 等编程语言，在 macOS 上使用 Linux 或 Windows 或 Docker 上的 SQL Server 生成应用。

下表列出了连接库或*驱动程序*客户端应用程序可以从各种语言连接到并使用 Microsoft SQL Server 运行在本地或云中、 在 Linux、 Windows 或 Docker 上使用和此外为 Azure SQL 数据库和 Azure SQL 数据仓库。 

| “报表” | 平台 | 其他资源 | 下载 | 开始操作 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [用于 SQL Server 的 Microsoft ADO.NET](http://msdn.microsoft.com/library/mt657768.aspx) | [下载](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows、Linux、macOS | [Microsoft JDBC Driver for SQL Server](http://msdn.microsoft.com/library/mt484311.aspx) | [下载](http://go.microsoft.com/fwlink/?LinkId=245496) |  [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows、Linux、macOS| [适用于 SQL Server 的 PHP SQL 驱动程序](../connect/php/microsoft-php-driver-for-sql-server.md) | 操作系统： <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows、Linux、macOS | [适用于 SQL Server 的 Node.js 驱动程序](../connect/node-js/node-js-driver-for-sql-server.md) |  [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows、Linux、macOS | [Python SQL 驱动程序](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows、Linux、macOS | [适用于 SQL Server 的 Ruby 驱动程序](../connect/ruby/ruby-driver-for-sql-server.md) | [入门](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows、Linux、macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [下载](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

下表列出了几个示例对象关系映射 (ORM) 框架和 web 框架的客户端应用程序可以使用运行的 Microsoft SQL Server 的本地或云中，在 Linux、 Windows 或 Docker 和 Azure SQL 数据库和Azure SQL 数据仓库。 

| “报表” | 平台 | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [实体框架](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows、Linux、macOS |[休眠 ORM](http://hibernate.org/orm)|
| PHP | Windows、Linux | [Laravel （配合）](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows、Linux、macOS | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | Windows、Linux、macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows、Linux、macOS | [Ruby on Rails](http://rubyonrails.org/) |

## <a name="related-links"></a>相关链接
- [SQL Server 驱动程序](http://msdn.microsoft.com/library/mt654049.aspx)从客户端应用程序连接
