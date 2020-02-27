---
title: 下载 Microsoft SQL Server JDBC 驱动程序
description: 下载 Microsoft JDBC Driver for SQL Server，以开发连接到 SQL Server 的 Java 应用程序。
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcf034b332494750885d4808b54c9cb62c37077c
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013112"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>下载 Microsoft SQL Server JDBC 驱动程序

本文收录了 Microsoft JDBC Driver for SQL Server 下载链接。 使用此驱动程序，可以开发连接到 SQL Server 的 Java 应用程序。  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>JDBC Driver for SQL Server 的可用下载

单击下表中的链接，可以下载与 Java Runtime Environment (JRE) 匹配的最新 Microsoft JDBC Driver for SQL Server：

| 版本 | 发布日期 | Java 版本 |
|---|---|---|
| [Microsoft JDBC Driver 8.2](https://go.microsoft.com/fwlink/?linkid=2116870) | 2020/1/31 | JRE 8、11、13 |
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 2019/8/1 | JRE 8、11、12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 2019/4/17 | JRE 8、11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 2018/7/31 | JRE 8、10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 2018/3/26 | JRE 7、8、9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 2018/2/12 | JRE 7、8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 2018/2/27 | JRE 7、8 |
| [Microsoft JDBC 驱动程序 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 2018/2/26 | JRE 7、8 |

下载此驱动程序时，有多个 JAR 文件。 JAR 文件名表示它支持的 Java 版本。 若要详细了解每个版本，请参阅[发行说明](release-notes-for-the-jdbc-driver.md)和[系统要求](system-requirements-for-the-jdbc-driver.md)。

## <a name="using-the-jdbc-driver-with-maven-central"></a>结合使用 JDBC 驱动程序与 Maven Central

JDBC 驱动程序可以添加到 Maven 项目，具体方法是通过使用以下代码将它作为依赖项添加到 POM.xml 文件中：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.0.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>不受支持的驱动程序

无法从此处下载不受支持的驱动程序版本。 我们在不断改善 Java 连接支持。 因此，强烈建议使用最新版 Microsoft JDBC Driver。  
  
## <a name="next-steps"></a>后续步骤

若要详细了解 Microsoft JDBC Driver for SQL Server，请参阅 [JDBC 驱动程序概述](overview-of-the-jdbc-driver.md)和 [JDBC 驱动程序 GitHub 存储库](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md)。
