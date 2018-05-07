---
title: 了解 JDBC 驱动程序数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 399037b5f888c767edf28c40c0658d31e8703ddc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-the-jdbc-driver-data-types"></a>了解 JDBC 驱动程序数据类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持 JDBC 内使用的 Java 应用程序的基本和高级数据类型的使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]作为其数据库。  
  
 JDBC 类型系统调解之间的转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据类型和 Java 语言类型和对象。 JDBC 类型的模型建立在 SQL-92 和 SQL-99 类型的基础之上。 JDBC 驱动程序符合 JDBC 规范，且设计为在可预测性与灵活性之间提供适当的平衡。  
  
 这部分的各个主题介绍如何使用基本数据类型和高级数据类型，以及如何可以将数据类型转换为其他数据类型。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[使用基本数据类型](../../connect/jdbc/using-basic-data-types.md)|描述 JDBC 基本数据类型。 包括一些示例，介绍如何通过结果集、参数化查询和存储过程来使用数据类型。|  
|[配置如何将 java.sql.Time 值发送到服务器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)|说明 JDBC 驱动程序如何生成日期。|  
|[使用高级数据类型](../../connect/jdbc/using-advanced-data-types.md)|描述 JDBC 高级数据类型。|  
|[了解数据类型的差异](../../connect/jdbc/understanding-data-type-differences.md)|描述不同 JDBC 驱动程序数据类型之间的差异。|  
|[了解数据类型转换](../../connect/jdbc/understanding-data-type-conversions.md)|描述当使用 getter 和 setter 方法时如何处理数据类型转换。|  
|[区域字符集支持](../../connect/jdbc/national-character-set-support.md)|介绍对区域字符集类型的支持。|  
|[支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)|介绍 SQLXML 接口。 此外介绍了如何读取和写入的 XML 数据的关系数据库到**SQLXML** Java 数据类型。|  
|[包装和接口](../../connect/jdbc/wrappers-and-interfaces.md)|讨论具有接口[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]特定的方法和常量允许应用程序服务器创建的代理类，还介绍了支持用于 java.sql.Wrapper 接口。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
