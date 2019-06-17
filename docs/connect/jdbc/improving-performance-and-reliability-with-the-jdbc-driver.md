---
title: 借助 JDBC 驱动程序提高性能和可靠性 | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b7cbadb13e5a14fe86a409cedfbffe98bb437e57
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781668"
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>借助 JDBC 驱动程序提高性能和可靠性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

所有应用程序开发的一个共同特点是需要不断地提高性能和可靠性。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了多种可帮助你实现这一点的技术。  
  
此部分中的主题说明了多种技术，可以在使用 JDBC 驱动程序时用于提高应用程序性能和可靠性。  

## <a name="in-this-section"></a>本节内容

|主题|描述|  
|-----------|-----------------|  
|[不使用时关闭对象](../../connect/jdbc/closing-objects-when-not-in-use.md)|说明不再需要 JDBC 驱动程序对象时将其关闭的重要性。|  
|[管理事务大小](../../connect/jdbc/managing-transaction-size.md)|说明用于提高事务性能的技术。|  
|[使用语句和结果集](../../connect/jdbc/working-with-statements-and-result-sets.md)|介绍用于使用的语句或结果集对象时提高性能的技术。|  
|[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)|介绍自适应缓冲功能，其作用是在无需服务器游标开销的情况下检索任何类型的大值数据。|  
|[稀疏列](../../connect/jdbc/sparse-columns.md)|介绍 JDBC 驱动程序对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稀疏列的支持。|  
|[JDBC 驱动程序的预处理语句元数据缓存](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|讨论可用于提高性能的已准备的语句查询技术。|
|[将大容量复制 API 用于批插入操作](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)|介绍如何为批处理插入操作和它的好处启用大容量复制 API。|

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
