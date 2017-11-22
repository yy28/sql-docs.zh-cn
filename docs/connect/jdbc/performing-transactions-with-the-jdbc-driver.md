---
title: "使用 JDBC 驱动程序执行事务 |Microsoft 文档"
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
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63dbf73c8100c1d4ab12ab80f1e7b6dcf6a5a6fa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>通过 JDBC 驱动程序执行事务
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  对于所有必须保证其永久性数据的一致性的应用程序而言，事务处理是必需要求。 与[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，事务处理可以本地执行或分发。 事务是原子级的、一致的、孤立的和持久的 (ACID) 执行模型。  
  
 本节中的主题介绍 JDBC 驱动程序如何支持包括隔离级别、事务保存点和结果集保持能力在内的事务。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[了解事务](../../connect/jdbc/understanding-transactions.md)|提供了如何通过 JDBC 驱动程序执行事务的概述。|  
|[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)|提供了如何通过 JDBC 驱动程序执行 XA 事务的概述。|  
|[了解隔离级别](../../connect/jdbc/understanding-isolation-levels.md)|介绍了 JDBC 驱动程序所支持的多种隔离级别。|  
|[使用保存点](../../connect/jdbc/using-savepoints.md)|介绍了如何结合事务保存点使用 JDBC 驱动程序。|  
|[使用可保持性](../../connect/jdbc/using-holdability.md)|介绍了如何结合结果集保持能力使用 JDBC 驱动程序。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
