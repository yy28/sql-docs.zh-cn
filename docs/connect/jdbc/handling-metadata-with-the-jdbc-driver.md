---
title: "处理元数据与 JDBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63d691c8bef93ad734a7596532ba567708128a2d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="handling-metadata-with-the-jdbc-driver"></a>使用 JDBC 驱动程序处理元数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可以用于处理元数据中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]各种不同的方式的数据库。 JDBC 驱动程序可用于获取数据库、结果集或参数的元数据。  
  
 JDBC 驱动程序提供三个类，用于检索元数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库：  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)，用于返回有关当前连接的数据库的信息。  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)，用于返回有关结果集的信息。  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)，用于返回已准备和可调用语句的参数信息。  
  
 此部分中的主题介绍如何使用三个元数据类中每个要使用元数据中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
> [!NOTE]  
>  就应用程序性能而言，本部分所讨论的元数据方法通常需要消耗大量资源，因此使用时应谨慎。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[使用数据库元数据](../../connect/jdbc/using-database-metadata.md)|说明如何检索有关当前已连接数据库的元数据信息。|  
|[使用结果设置元数据](../../connect/jdbc/using-result-set-metadata.md)|说明如何检索有关当前结果集的元数据信息。|  
|[使用参数元数据](../../connect/jdbc/using-parameter-metadata.md)|说明如何检索有关预定义语句参数和可调用语句参数的元数据信息。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

