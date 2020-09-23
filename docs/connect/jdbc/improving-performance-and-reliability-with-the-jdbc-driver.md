---
title: 通过 JDBC 驱动程序提升性能和可靠性
description: 了解多种技术，以便在使用 Microsoft JDBC Driver for SQL Server 时用于提高应用程序性能和可靠性。
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc04a90569974acbc99dcb66680d66289db1c0d1
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565375"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>通过 JDBC 驱动程序提升性能和可靠性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

所有应用程序开发的一个共同特点是需要不断地提高性能和可靠性。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了多种可帮助你实现这一点的技术。  
  
此部分中的主题说明了多种技术，可以在使用 JDBC 驱动程序时用于提高应用程序性能和可靠性。  

## <a name="in-this-section"></a>在本节中

|主题|说明|  
|-----------|-----------------|  
|[不使用时关闭对象](../../connect/jdbc/closing-objects-when-not-in-use.md)|说明不再需要 JDBC 驱动程序对象时将其关闭的重要性。|  
|[管理事务大小](../../connect/jdbc/managing-transaction-size.md)|说明用于提高事务性能的技术。|  
|[处理语句和结果集](../../connect/jdbc/working-with-statements-and-result-sets.md)|介绍在使用 Statement 或 ResultSet 对象时可用于提高性能的技术。|  
|[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)|介绍自适应缓冲功能，其作用是在无需服务器游标开销的情况下检索任何类型的大值数据。|  
|[稀疏列](../../connect/jdbc/sparse-columns.md)|介绍 JDBC 驱动程序对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稀疏列的支持。|  
|[JDBC 驱动程序的预处理语句元数据缓存](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|讨论用预定义语句查询提高性能的方法。|
|[将大容量复制 API 用于批量插入操作](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|介绍如何为批处理插入操作启用大容量复制 API 以及这样做的优点。|
|[不以 Unicode 格式发送 String 参数](../../connect/jdbc/setting-the-connection-properties.md)|在使用 CHAR、VARCHAR 和 LONGVARCHAR 数据时，用户可以将连接属性 sendStringParametersAsUnicode 设置为 `false`，以获得最佳性能提升。|

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
