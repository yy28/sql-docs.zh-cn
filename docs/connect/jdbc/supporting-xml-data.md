---
title: "支持 XML 数据 |Microsoft 文档"
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
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77ec535a43cf79b10e25d3c0fd7108d3c9a40dd0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="supporting-xml-data"></a>支持 XML 数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]提供**xml** ，您可以存储 XML 文档和片段中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 **Xml**数据类型是中的内置数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并在某些方面类似于其他内置类型，如是**int**和**varchar**。 像其他内置类型，你可以使用**xml**数据类型为： 当你创建表; 或键入变量的类型、 参数类型、 函数返回类型或列[!INCLUDE[tsql](../../includes/tsql_md.md)]CAST 和 CONVERT 函数。 JDBC 驱动程序中, **xml**可以作为字符串、 字节数组、 流、 CLOB、 BLOB 或 SQLXML 对象映射数据类型。 字符串是默认映射。  
  
 JDBC 驱动程序提供对 JDBC 4.0 API 的支持，后者引入了 SQLXML 接口。 SQLXML 接口定义与 XML 数据交互以及操作 XML 数据的方法。 **SQLXML** JDBC 4.0 数据类型，它映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**数据类型。 因此，如果要在应用程序中使用 SQLXML 数据类型，必须将 classpath 设置为包含 sqljdbc4.jar 文件。 如果应用程序在访问 SQLXML 对象及其方法时尝试使用 sqljdbc3.jar，将引发异常。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]始终将它存储在数据库列之前验证的 XML 数据。 应用程序可以使用**SQLXML**数据类型，因为 JDBC 驱动程序将其映射到**xml**自动数据类型。 **SQLXML** sqljdbc4.jar 中提供了支持。 请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)有关支持的 JRE 版本的列表[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 此部分中的主题描述 SQLXML 接口以及如何对其进行编程**SQLXML**使用 JDBC API 方法的数据类型。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[SQLXML 接口](../../connect/jdbc/sqlxml-interface.md)|介绍 SQLXML 接口及其方法。|  
|[使用 SQLXML 进行编程](../../connect/jdbc/programming-with-sqlxml.md)|介绍如何使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]API 方法来存储和检索 XML 数据从关系数据库中的和**SQLXML** Java 数据类型。 此外还包含有关 SQLXML 对象类型的信息，并提供使用 SQLXML 对象的重要准则和限制的列表。|  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
