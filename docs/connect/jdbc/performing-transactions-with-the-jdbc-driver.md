---
title: 通过 JDBC 驱动程序执行事务 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa86cde4d8c7d0aa91b5864f5beb3317b91bf0ee
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923743"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>通过 JDBC 驱动程序执行事务
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  对于所有必须保证其永久性数据的一致性的应用程序而言，事务处理是必需要求。 通过 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，可以在本地或以分散的方式执行事务处理。 事务是原子级的、一致的、孤立的和持久的 (ACID) 执行模型。  
  
 本节中的主题介绍 JDBC 驱动程序如何支持包括隔离级别、事务保存点和结果集保持能力在内的事务。  
  
## <a name="in-this-section"></a>在本节中  
  
|主题|说明|  
|-----------|-----------------|  
|[了解事务](../../connect/jdbc/understanding-transactions.md)|提供了如何通过 JDBC 驱动程序执行事务的概述。|  
|[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)|提供了如何通过 JDBC 驱动程序执行 XA 事务的概述。|  
|[了解隔离级别](../../connect/jdbc/understanding-isolation-levels.md)|介绍了 JDBC 驱动程序所支持的多种隔离级别。|  
|[使用保存点](../../connect/jdbc/using-savepoints.md)|介绍了如何结合事务保存点使用 JDBC 驱动程序。|  
|[使用可保持性](../../connect/jdbc/using-holdability.md)|介绍了如何结合结果集保持能力使用 JDBC 驱动程序。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
