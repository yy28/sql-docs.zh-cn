---
title: Always Encrypted（客户端开发）| Microsoft Docs
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b6cd19272cc7c8c3f7129b3089c7ae575350b52e
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698248"
---
# <a name="always-encrypted-client-development"></a>始终加密（客户端开发）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[始终加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)是可确保敏感数据（和相关的加密密钥）永远不会泄露到 SQL Server 或 Azure SQL 数据库的客户端加密技术。 通过“始终加密”，客户端驱动程序可在将敏感数据传至数据库引擎之前对其以透明方式加密，并对从加密数据库列中检索的数据以透明方式解密。

有关开发使用受“始终加密”技术保护的数据库的应用程序以及哪些客户端驱动程序和哪些驱动程序版本支持“始终加密”的详细信息，请参阅：

- [对用于 SQL Server 的 .NET Framework 数据提供程序使用 Always Encrypted](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [对 JDBC 驱动程序使用始终加密](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [对 Windows ODBC 驱动程序使用始终加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)



## <a name="see-also"></a>另请参阅

[始终加密（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)

