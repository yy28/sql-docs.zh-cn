---
title: 支持 XML 数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f98ef1cbff732bc969b8eea45ad38ee2f158fa73
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622055"
---
# <a name="supporting-xml-data"></a>支持 XML 数据
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了 xml 数据类型，该数据类型允许将 XML 文档和片段存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中。 xml 数据类型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的内置数据类型，在某些方面类似于其他内置类型（如 int 和 varchar）。 与其他内置类型一样，在创建表时或者在 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 和 CONVERT 函数中，可以将 xml 数据类型用作变量类型、参数类型、函数返回类型或列类型。 在 JDBC 驱动程序中，xml 数据类型可以映射为字符串、字节数组、流、CLOB、BLOB 或 SQLXML 对象。 字符串是默认映射。  
  
 JDBC 驱动程序提供对 JDBC 4.0 API 的支持，后者引入了 SQLXML 接口。 SQLXML 接口定义与 XML 数据交互以及操作 XML 数据的方法。 **SQLXML**是 JDBC 4.0 数据类型，它映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml**数据类型。 因此，如果要在应用程序中使用 SQLXML 数据类型，必须将 classpath 设置为包含 sqljdbc4.jar 文件。 如果应用程序在访问 SQLXML 对象及其方法时尝试使用 sqljdbc3.jar，将引发异常。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在将 XML 数据存储到数据库列中之前，始终会对其进行验证。 应用程序可以使用 SQLXML 数据类型，因为 JDBC 驱动程序会自动将它映射为 xml 数据类型。 sqljdbc4.jar 中提供了 SQLXML 支持。 请参阅[JDBC 驱动程序的系统要求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)支持的 JRE 版本的列表[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 本节中的主题介绍 SQLXML 接口，并说明如何使用 JDBC API 方法来针对 SQLXML 数据类型进行编程。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|描述|  
|-----------|-----------------|  
|[SQLXML 接口](../../connect/jdbc/sqlxml-interface.md)|介绍 SQLXML 接口及其方法。|  
|[使用 SQLXML 进行编程](../../connect/jdbc/programming-with-sqlxml.md)|介绍如何使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API 方法在具有 SQLXML Java 数据类型的关系数据库中存储和检索 XML 数据。 此外还包含有关 SQLXML 对象类型的信息，并提供使用 SQLXML 对象的重要准则和限制的列表。|  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
