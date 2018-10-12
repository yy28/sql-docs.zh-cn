---
title: 获取驱动程序版本 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7abc69edd0d49264a62ea0c3f65a60b58549d105
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774215"
---
# <a name="getting-the-driver-version"></a>获取驱动程序版本
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以通过以下方法找到已安装 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的版本：  
  
-   调用 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 方法 [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)、[getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) 或 [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)。  
  
-   版本将显示在产品分发内容的 readme.txt 文件中。  
  
 此外，可以通过在 SQLServerDatabaseMetaData 类上调用 [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) 方法来返回 JDBC 驱动程序名称。 例如，将返回“Microsoft JDBC Driver 6.4 for SQL Server”。  
  
 下面是输出的从对 SQLServerDatabaseMetaData 类方法的调用示例：  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 其中，“xxx.x”是最终版本号。  
  
## <a name="see-also"></a>另请参阅  
 [诊断与 JDBC 驱动程序有关的问题](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
