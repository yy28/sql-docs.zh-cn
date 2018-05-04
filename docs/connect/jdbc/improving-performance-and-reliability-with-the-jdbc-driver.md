---
title: 提高性能和可靠性使用 JDBC 驱动程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c67e4b53413d1d40a4a92664dc75c91d8a21525
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>借助 JDBC 驱动程序提高性能和可靠性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  所有应用程序开发的一个共同特点是需要不断地提高性能和可靠性。 有大量技术来实现这一点与[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 此部分中的主题说明了多种技术，可以在使用 JDBC 驱动程序时用于提高应用程序性能和可靠性。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[不使用时关闭对象](../../connect/jdbc/closing-objects-when-not-in-use.md)|说明不再需要 JDBC 驱动程序对象时将其关闭的重要性。|  
|[管理事务大小](../../connect/jdbc/managing-transaction-size.md)|说明用于提高事务性能的技术。|  
|[使用语句和结果集](../../connect/jdbc/working-with-statements-and-result-sets.md)|描述用于使用的语句或结果集的对象时提高性能的技术。|  
|[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)|介绍自适应缓冲功能，其作用是在无需服务器游标开销的情况下检索任何类型的大值数据。|  
|[稀疏列](../../connect/jdbc/sparse-columns.md)|讨论对适用的 JDBC 驱动程序的支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]稀疏列。|  
|[JDBC 驱动程序的预处理语句元数据缓存](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|讨论用于使用已准备的语句查询提高性能的技术。|
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  