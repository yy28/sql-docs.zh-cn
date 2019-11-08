---
title: 使用 Always Encrypted 开发应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 235dc20ca94affa5f022bc242aa0ef6726f1542c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594448"
---
# <a name="develop-applications-using-always-encrypted"></a>使用 Always Encrypted 开发应用程序
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[始终加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)是可确保敏感数据（和相关的加密密钥）永远不会泄露到 SQL Server 或 Azure SQL 数据库的客户端加密技术。 通过“始终加密”，客户端驱动程序可在将敏感数据传至数据库引擎之前对其以透明方式加密，并对从加密数据库列中检索的数据以透明方式解密。

有关开发使用受“始终加密”技术保护的数据库的应用程序以及哪些客户端驱动程序和哪些驱动程序版本支持“始终加密”的详细信息，请参阅：

- [对用于 SQL Server 的 .NET Framework 数据提供程序使用 Always Encrypted](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [对 JDBC 驱动程序使用始终加密](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [对 ODBC 驱动程序使用 Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [对 PHP 驱动程序使用 Always Encrypted](../../../connect/php/using-always-encrypted-php-drivers.md)
- [在 .NET Core 和 .NET Framework 应用程序中对 Microsoft.Data.SqlClient 使用 Always Encrypted](https://github.com/dotnet/sqlclient/tree/master/release-notes)
- [始终加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
