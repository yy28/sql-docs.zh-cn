---
title: "使用大数据 |Microsoft 文档"
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
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f21be61a9e91f3c3bbe0f5ab82c81435b57ef29e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-large-data"></a>处理大型数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驱动程序提供自适应缓冲支持，使您可以在无需服务器游标开销的情况下检索任何类型的大值数据。 使用自适应缓冲[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]检索语句执行结果从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]随着应用程序需要它们，而不是一次。 一旦应用程序不再访问结果，驱动程序还会立即丢弃它们。  
  
 在[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] JDBC 驱动程序版本 1.2，缓冲模式处于"**完整**"默认情况下。 如果你的应用程序未不将"responseBuffering"连接属性设置为"**自适应**"的连接属性中或通过使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象、 驱动程序支持在一次从服务器读取整个结果。 为了获取自适应缓冲行为，你的应用程序必须将"responseBuffering"连接属性设置为"**自适应**"显式。  
  
 **自适应**值是默认设置缓冲模式和 JDBC 驱动程序将缓冲区的最小可能的数据在必要时。 有关使用自适应缓冲的详细信息，请参阅[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)。  
  
 此部分中的主题描述了可用于检索从大值数据的不同方式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[读取大型数据的示例](../../connect/jdbc/reading-large-data-sample.md)|说明如何使用 SQL 语句检索大值数据。|  
|[使用存储过程读取大型数据的示例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|说明如何检索大型 CallableStatement OUT 参数值。|  
|[更新大型数据的示例](../../connect/jdbc/updating-large-data-sample.md)|说明如何更新数据库中的大值数据。|  
  
## <a name="see-also"></a>另请参阅  
 [示例 JDBC 驱动程序应用程序](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
