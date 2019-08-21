---
title: 使用大型数据 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aab60ed1db5d7749c4edbc52fcad4bebddf93d52
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025466"
---
# <a name="working-with-large-data"></a>处理大型数据

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

JDBC 驱动程序提供自适应缓冲支持，使您可以在无需服务器游标开销的情况下检索任何类型的大值数据。 借助自适应缓冲，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 可以在应用程序需要时从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中检索语句执行结果，而不是一次性检索全部结果。 一旦应用程序不再访问结果，驱动程序还会立即丢弃它们。

在 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] JDBC Driver 1.2 版中，缓冲模式默认为“full”  。 如果应用程序没有将“responseBuffering”连接属性设置为“adaptive”  （在连接属性中或使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法），驱动程序支持一次性从服务器中读取全部结果。 应用程序必须将“responseBuffering”连接属性显式设置为“adaptive”  ，才能获取自适应缓冲行为。  
  
adaptive  值是默认缓冲模式，JDBC Driver 在必要时缓冲尽可能少的数据。 有关使用自适应缓冲的详细信息, 请参阅[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)。  
  
 此部分中的主题介绍了各种用于从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库检索大值数据的方法。  
  
## <a name="in-this-section"></a>本节内容  
  
| 主题                                                                                                                      | 描述                                                              |
| -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [读取大型数据的示例](../../connect/jdbc/reading-large-data-sample.md)                                               | 说明如何使用 SQL 语句检索大值数据。       |
| [使用存储过程读取大型数据的示例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md) | 说明如何检索大型 CallableStatement OUT 参数值。 |
| [更新大型数据的示例](../../connect/jdbc/updating-large-data-sample.md)                                             | 说明如何更新数据库中的大值数据。                |
  
## <a name="see-also"></a>另请参阅

[示例 JDBC 驱动程序应用程序](../../connect/jdbc/sample-jdbc-driver-applications.md)  
