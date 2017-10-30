---
title: "获取驱动程序版本 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2322c3ece650fb05fe19fd55e36f79e73db7d32d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getting-the-driver-version"></a>获取驱动程序版本
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  已安装的版本[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可以通过以下方式找到：  
  
-   调用[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)方法[getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)， [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)，或[getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)。  
  
-   版本将显示在产品分发内容的 readme.txt 文件中。  
  
 此外，从返回的 JDBC 驱动程序名称[getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) SQLServerDatabaseMetaData 类上的方法调用。 例如，将返回“Microsoft JDBC Driver 4.0 for SQL Server”。  
  
 下面是从对 SQLServerDatabaseMetaData 类的方法调用的输出示例：  
  
 `getDriverName = Microsoft JDBC Driver 4.0 for SQL Server`  
  
 `getDriverMajorVersion = 4`  
  
 `getDriverMinorVersion = 0`  
  
 `getDriverVersion = 4.0.`*xxx.x*  
  
 其中，“xxx.x”是最终版本号。  
  
## <a name="see-also"></a>另请参阅  
 [诊断 JDBC 驱动程序的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  

