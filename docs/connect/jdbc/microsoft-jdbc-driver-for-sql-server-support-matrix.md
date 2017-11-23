---
title: "Microsoft JDBC Driver for SQL Server 支持矩阵 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9867704e5fe3b5522d22c70cc1b79b495de1bfa5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Microsoft SQL Server JDBC 驱动程序支持矩阵
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本页包含 Microsoft SQL Server JDBC 驱动程序的支持矩阵和支持生命周期策略。  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Microsoft JDBC 驱动程序支持生命周期矩阵和策略  
 Microsoft 支持生命周期 (MSL) 策略提供了与 Microsoft 产品的支持生命周期有关的可预测透明信息。 自驱动程序发布之日起，JDBC 驱动程序 3.0 版和 4.x 版就具有五年的主流支持。 主流支持在 Microsoft 支持生命周期网站上定义。  
  
 Microsoft JDBC 驱动程序不提供扩展和自定义支持选项。  
    
 支持以下 Microsoft JDBC 驱动程序，直到指定的支持结束日期。  
  
|驱动程序名称|驱动程序包版本|适用的 JAR(s)|终止主流支持|
|-|-|-|-|  
|Microsoft JDBC Driver 6.2 for SQL Server|6.2|mssql jdbc 6.2.2.jre8.jar<br> mssql jdbc 6.2.2.jre7.jar|2022 年 6 月 30 日|    
|Microsoft JDBC Driver 6.0 for SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|2021 年 7 月 14 日|    
|Microsoft SQL Server JDBC 驱动程序 4.2|4.2|sqljdbc42.jar<br>sqljdbc41.jar|2020 年 8 月 24 日|  
|Microsoft SQL Server JDBC 驱动程序 4.1|4.1|sqljdbc41.jar|2019 年 12 月 12 日|  
  
 以下 Microsoft JDBC 驱动程序不再受到支持。  
 
|驱动程序名称|驱动程序包版本|终止主流支持|  
|-|-|-|
|Microsoft JDBC Driver 4.0 for SQL Server|4.0|2017 年 3 月 6 日|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|2015 年 4 月 23 日|  
|Microsoft SQL Server JDBC 驱动程序 2.0|2.0|2012 年 12 月 31 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.2|1.2|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC 驱动程序 1.1|1.1|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC 驱动程序 1.0|1.0|2011 年 6 月 25 日|  
|Microsoft SQL Server 2000 JDBC 驱动程序|2000|2010 年 7 月 9 日|  
  
## <a name="sql-version-compatibility"></a>SQL 版本兼容性  
  
|驱动程序版本|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Azure SQL Database|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|  
|-|-|-|-|-|-|-|-|-| 
|6.2|是|是|是|是|是|是|是|是|  
|6.1|是|是|是|是|是|是|是|否|  
|6.0|是|是|是|是|是|是|是|否|  
|4.2|是|是|是|是|是|是|是|否|  
|4.1|是|是|是|是|是|是|是|否|  
|4.0|是|是|是|是|是|是|是|否|  
|3.0|是|是|Y<sup>1</sup>|Y<sup>2</sup>|否|Y<sup>5</sup>|否|否|  
|2.0|Y<sup>3</sup>|Y<sup>3</sup>|否|否|否|否|否|否|  
|1.2|Y<sup>3</sup>|否|否|否|否|否|否|否|  
|1.1|否|否|否|否|否|否|否|否|  
|1.0|否|否|否|否|否|否|否|否|  
|2000|否|否|否|否|否|否|否|否|  
  
 <sup>1</sup>Microsoft SQL Server JDBC 驱动程序版本 3.0 可以连接到 SQL Server 2012 作为下层客户端。  
  
 <sup>2</sup>作为修补程序 3.0 的驱动程序中引入了对 Azure SQL 数据库支持。 建议 Azure SQL Database 客户使用最新的驱动程序版本。  
  
 <sup>3</sup>Microsoft SQL Server JDBC 驱动程序版本 2.0 和 Microsoft SQL Server 2005 JDBC 驱动程序版本 1.2 可以连接到 SQL Server 2008 为下层客户端。 当允许下级转换时，应用程序可以对新的 SQL Server 2008 数据类型执行查询和更新，如 time、date、datetime2、datetimeoffset 和 FILESTREAM。 有关如何将这些新数据类型用于 JDBC 驱动程序的详细信息，请参阅  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver（使用 JDBC 驱动程序处理 SQL Server 2008 日期/时间数据类型）](http://go.microsoft.com/fwlink/?LinkId=145198) 和  [Working with SQL Server 2008 FileStream using JDBC Driver（使用 JDBC 驱动程序处理 SQL Server 2008 文件流）](http://go.microsoft.com/fwlink/?LinkId=145199)。 有关这些新数据类型的下级兼容性的详细信息，请参阅 SQL Server 联机丛书中的  [Using Date and Time Data（使用日期和时间数据）](http://go.microsoft.com/fwlink/?LinkId=145211)和  [FILESTREAM Support（文件流支持）](http://go.microsoft.com/fwlink/?LinkId=145212) 主题。  
  
 <sup>4</sup>Microsoft JDBC 驱动程序和并行数据仓库之间的连接首先中引入了支持 Microsoft JDBC Driver 4.0 for SQL Server 和 Microsoft SQL Server 2008 R2 并行数据仓库设备更新 3。  
  
 <sup>5</sup>Microsoft SQL Server JDBC 驱动程序版本 3.0 可以连接到 SQL Server 2014 作为下层客户端。  
  
## <a name="java-and-jdbc-specification-support"></a>Java 和 JDBC 规格支持  
  
|JDBC 驱动程序版本|JRE 版本|JDBC API 版本| 
|-|-|-|  
|6.2|1.7, 1.8|4.1, 4.2|  
|6.1|1.7, 1.8|4.1, 4.2|  
|6.0|1.7, 1.8|4.1, 4.2|  
|4.2|1.7, 1.8|4.1, 4.2|  
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
  
 JDBC 产品团队在 Windows、Sun Solaris、SUSE Linux 和 RedHat Linux 上测试了驱动程序。  所有平台都提供客户支持，但我们可能会要求你在 Windows 等平台上重现问题。  
  
## <a name="application-server-support"></a>应用程序服务器支持  
 针对各种应用程序服务器对 Microsoft SQL Server JDBC 驱动程序进行了测试。  请咨询应用程序服务器供应商了解有关与其产品兼容的驱动程序版本的其他详细信息。  
  
  
