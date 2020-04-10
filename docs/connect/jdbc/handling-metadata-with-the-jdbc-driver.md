---
title: 通过 JDBC 驱动程序处理元数据 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 859932404e14a9ab1216665d211e1b6734ca9726
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924690"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>通过 JDBC 驱动程序处理元数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以通过多种方式使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的元数据。 JDBC 驱动程序可用于获取数据库、结果集或参数的元数据。  
  
 JDBC 驱动程序提供了三个从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中检索元数据的类：  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)，用于返回有关当前已连接的数据库的信息。  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)，用于返回有关结果集的信息。  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)，用于返回有关预定义且可调用语句的参数的信息。  
  
 本部分中的主题介绍了如何使用这三个元数据类来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的元数据。  
  
> [!NOTE]  
>  就应用程序性能而言，本部分所讨论的元数据方法通常需要消耗大量资源，因此使用时应谨慎。  
  
## <a name="in-this-section"></a>在本节中  
  
|主题|说明|  
|-----------|-----------------|  
|[使用数据库元数据](../../connect/jdbc/using-database-metadata.md)|说明如何检索有关当前已连接数据库的元数据信息。|  
|[使用结果集元数据](../../connect/jdbc/using-result-set-metadata.md)|说明如何检索有关当前结果集的元数据信息。|  
|[使用参数元数据](../../connect/jdbc/using-parameter-metadata.md)|说明如何检索有关预定义语句参数和可调用语句参数的元数据信息。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
