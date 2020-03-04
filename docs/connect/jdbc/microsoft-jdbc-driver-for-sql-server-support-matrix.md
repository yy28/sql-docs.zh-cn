---
title: Microsoft JDBC Driver for SQL Server 支持矩阵 | Microsoft Docs
ms.custom: ''
ms.date: 02/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa431aa3787c0929484667c378585fa85d0ce17c
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903694"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Microsoft JDBC Driver for SQL Server 支持矩阵
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本页包含 Microsoft SQL Server JDBC 驱动程序的支持矩阵和支持生命周期策略。  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Microsoft JDBC Driver 支持生命周期矩阵和策略  
 Microsoft 支持生命周期 (MSL) 策略提供了与 Microsoft 产品的支持生命周期有关的可预测透明信息。 自驱动程序发布之日起，JDBC Driver 3.0 版、4.x 版、6.x 版、7.x 版和 8.x 版就具有五年的主流支持。 主流支持在 Microsoft 支持生命周期网站上定义。  
  
 Microsoft JDBC 驱动程序不提供扩展和自定义支持选项。  
    
 支持以下 Microsoft JDBC 驱动程序，直到指定的支持结束日期。  
  
|驱动程序名称|驱动程序包版本|适用的 JAR|主要支持结束日期|
|-|-|-|-|  
|Microsoft JDBC Driver 8.2 for SQL Server|8.2|mssql-jdbc-8.2.1.jre13.jar<br> mssql-jdbc-8.2.1.jre11.jar<br> mssql-jdbc-8.2.1.jre8.jar|2025 年 2 月 26 日|
|Microsoft JDBC Driver 7.4 for SQL Server|7.4|mssql-jdbc-7.4.1.jre12.jar<br> mssql-jdbc-7.4.1.jre11.jar<br> mssql-jdbc-7.4.1.jre8.jar|2024 年 8 月 2 日|
|Microsoft JDBC Driver 7.2 for SQL Server|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|2024 年 4 月 16 日|
|Microsoft JDBC Driver 7.0 for SQL Server|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|2023 年 7 月 31 日|  
|Microsoft JDBC Driver 6.4 for SQL Server|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|2023 年 2 月 27 日|    
|Microsoft JDBC Driver 6.2 for SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|2022 年 6 月 30 日|    
|Microsoft JDBC Driver 6.0 for SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|2021 年 7 月 14 日|    
|Microsoft SQL Server JDBC 驱动程序 4.2|4.2|sqljdbc42.jar<br>sqljdbc41.jar|2020 年 8 月 24 日|  
  
 以下 Microsoft JDBC 驱动程序不再受到支持。  
 
|驱动程序名称|驱动程序包版本|主要支持结束日期|  
|-|-|-|
|Microsoft SQL Server JDBC 驱动程序 4.1|4.1|2019 年 12 月 12 日| 
|Microsoft JDBC Driver 4.0 for SQL Server|4.0|2017 年 3 月 6 日|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|2015 年 4 月 23 日|  
|Microsoft SQL Server JDBC 驱动程序 2.0|2.0|2012 年 12 月 31 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.2|1.2|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC 驱动程序 1.1|1.1|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC 驱动程序 1.0|1.0|2011 年 6 月 25 日|  
|Microsoft SQL Server 2000 JDBC 驱动程序|2000|2010 年 7 月 9 日|  
  
## <a name="sql-version-compatibility"></a>SQL 版本兼容性  
  
|驱动程序版本|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Azure SQL 数据库|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Server 2019|  
|-|-|-|-|-|-|-|-|-|-|-|
|8.2|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.4|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.2|N|Y|Y|Y|Y|Y|Y|Y|N| 
|7.0|N|Y|Y|Y|Y|Y|Y|Y|N| 
|6.4|N|Y|Y|Y|Y|Y|Y|Y|N| 
|6.2|Y|Y|Y|Y|Y|Y|Y|Y|N|
|6.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|6.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.2|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|3.0|Y|Y|是<sup>1</sup>|是<sup>2</sup>|N|是<sup>5</sup>|N|N|N|
|2.0|是<sup>3</sup>|是<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|是<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|  
|1.0|N|N|N|N|N|N|N|N|N|  
|2000|N|N|N|N|N|N|N|N|N|  
  
 <sup>1</sup>Microsoft SQL Server JDBC 驱动程序 3.0 版可作为下级客户端连接到 SQL Server 2012。  
  
 <sup>2</sup>3.0 驱动程序中以修补程序的形式引入了 Azure SQL Database 的支持。 建议 Azure SQL Database 客户使用最新的驱动程序版本。  
  
 <sup>3</sup>Microsoft SQL Server JDBC 驱动程序 2.0 版和 Microsoft SQL Server 2005 JDBC 驱动程序 1.2 版可作为下级客户端连接到 SQL Server 2008。 当允许下级转换时，应用程序可以对新的 SQL Server 2008 数据类型执行查询和更新，如 time、date、datetime2、datetimeoffset 和 FILESTREAM。 有关如何将这些新数据类型用于 JDBC 驱动程序的详细信息，请参阅  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver（使用 JDBC 驱动程序处理 SQL Server 2008 日期/时间数据类型）](https://go.microsoft.com/fwlink/?LinkId=145198) 和  [Working with SQL Server 2008 FileStream using JDBC Driver（使用 JDBC 驱动程序处理 SQL Server 2008 文件流）](https://go.microsoft.com/fwlink/?LinkId=145199)。 有关这些新数据类型的下级兼容性的详细信息，请参阅 SQL Server 联机丛书中的  [Using Date and Time Data（使用日期和时间数据）](https://go.microsoft.com/fwlink/?LinkId=145211)和  [FILESTREAM Support（文件流支持）](https://go.microsoft.com/fwlink/?LinkId=145212) 主题。  
  
 <sup>4</sup>Microsoft SQL Server JDBC 驱动程序 4.0 和 Microsoft SQL Server 2008 R2 并行数据仓库设备更新 3 中首先引入了 Microsoft JDBC 驱动程序和并行数据仓库间的连接支持。  
  
 <sup>5</sup>Microsoft SQL Server JDBC 驱动程序 3.0 版可作为下级客户端连接到 SQL Server 2014。  
  
## <a name="java-and-jdbc-specification-support"></a>Java 和 JDBC 规格支持  
  
|JDBC 驱动程序版本|JRE 版本|JDBC API 版本| 
|-|-|-|  
|8.2|1.8、11、13|4.2、4.3（部分）|
|7.4|1.8、11、12|4.2、4.3（部分）|
|7.2|1.8、11|4.2、4.3（部分）|
|7.0|1.8、10|4.2、4.3（部分）|
|6.4|1.7、1.8、9|4.1、4.2、4.3（部分）|  
|6.2|1.7、1.8|4.1、4.2|  
|6.1|1.7、1.8|4.1、4.2|  
|6.0|1.7、1.8|4.1、4.2|  
|4.2|1.7、1.8|4.1、4.2|  
|4.1|1.7|4.0|  
|4.0|1.5、1.6、1.7|3.0、4.0|  
|3.0|1.5、1.6、|3.0、4.0|  
|2.0|1.5、1.6|3.0、4.0|  
|1.2|1.4、1.5、1.6|3.0|  
|1.1|1.4|3.0|  
|1.0|1.4|3.0|  
|2000|1.4|3.0|  
  
## <a name="supported-operating-systems"></a>支持的操作系统  
 Microsoft JDBC 驱动程序可在任何支持使用 Java 虚拟机 (JVM) 的操作系统上工作。 一些常用的平台包括 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 R2、Windows Vista、Linux、Unix、AIX、MacOS 等。  
  
 JDBC 产品团队在 Windows、Sun Solaris、SUSE Linux、Ubuntu Linux、CentOS Linux 和 macOS 上测试了驱动程序。
## <a name="application-server-support"></a>应用程序服务器支持  
 针对各种应用程序服务器对 Microsoft SQL Server JDBC 驱动程序进行了测试。  请咨询应用程序服务器供应商了解有关与其产品兼容的驱动程序版本的其他详细信息。
 
 
