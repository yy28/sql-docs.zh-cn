---
title: 了解 JDBC 驱动程序数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15ecca3277dcba3cd2235da9bff9a8d9fc2e4f6f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920276"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>了解 JDBC 驱动程序数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支持在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为数据库的 Java 应用程序中使用 JDBC 的基本数据类型和高级数据类型。  
  
JDBC 类型系统负责调解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型与 Java 语言类型和对象之间的转换。 JDBC 类型的模型建立在 SQL-92 和 SQL-99 类型的基础之上。 JDBC 驱动程序符合 JDBC 规范，且设计为在可预测性与灵活性之间提供适当的平衡。  
  
这部分的各个主题介绍如何使用基本数据类型和高级数据类型，以及如何可以将数据类型转换为其他数据类型。  
  
## <a name="in-this-section"></a>在本节中  
  
| 主题                                                                                                                                            | 说明                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [使用基本数据类型](../../connect/jdbc/using-basic-data-types.md)                                                                           | 描述 JDBC 基本数据类型。 包括一些示例，介绍如何通过结果集、参数化查询和存储过程来使用数据类型。                                                                                                        |
| [配置 java.sql.Time 值发送到服务器的方式](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md) | 说明 JDBC 驱动程序如何生成日期。                                                                                                                                                                                                                       |
| [使用高级数据类型](../../connect/jdbc/using-advanced-data-types.md)                                                                     | 描述 JDBC 高级数据类型。                                                                                                                                                                                                                              |
| [了解数据类型区别](../../connect/jdbc/understanding-data-type-differences.md)                                                 | 描述不同 JDBC 驱动程序数据类型之间的差异。                                                                                                                                                                                                    |
| [了解数据类型转换](../../connect/jdbc/understanding-data-type-conversions.md)                                                 | 描述当使用 getter 和 setter 方法时如何处理数据类型转换。                                                                                                                                                                                  |
| [区域字符集支持](../../connect/jdbc/national-character-set-support.md)                                                           | 介绍对区域字符集类型的支持。                                                                                                                                                                                                          |
| [支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)                                                                                 | 介绍 SQLXML 接口。 此外还说明了如何使用 SQLXML Java 数据类型在关系数据库中读取和写入 XML 数据  。                                                                                                             |
| [包装器和接口](../../connect/jdbc/wrappers-and-interfaces.md)                                                                         | 论述具有允许应用程序服务器创建类代理的 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的方法和常量的接口，还论述对 `java.sql.Wrapper` 接口的支持。 |
  
## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
