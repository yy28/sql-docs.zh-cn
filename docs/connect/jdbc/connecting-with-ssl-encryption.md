---
title: 使用加密进行连接 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cff4228404690147d97a44f6f5dd43b1a180153c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "71713296"
---
# <a name="connecting-with-encryption"></a>使用加密进行连接
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本文中的示例描述如何使用连接字符串属性允许应用程序在 Java 应用程序中使用传输层安全性 (TLS) 加密。 有关这些新的连接字符串属性（如 encrypt、trustServerCertificate、trustStore、trustStorePassword 和 hostNameInCertificate）的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)      。  
  
 当 encrypt 属性设置为 true 且 trustServerCertificate 属性设置为 true 时，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将不验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TLS 证书     。 这一点对于允许在测试环境中建立连接通常是必需的，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例只具有自签名证书的情况。  
  
 下面的代码示例演示如何在连接字符串中设置 trustServerCertificate 属性  ：  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 当 encrypt 属性设置为 true 且 trustServerCertificate 属性设置为 false 时，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TLS 证书     。 验证服务器证书是 TLS 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 为了验证服务器证书，在连接时必须提供信任材料，既可以使用 trustStore 和 trustStorePassword 连接属性显式提供材料，也可以使用基础 Java 虚拟机 (JVM) 的默认信任存储区隐式提供材料   。  
  
 trustStore 属性指定指向证书 trustStore 文件的路径（包括文件名），该文件中包含客户端信任的证书的列表  。 trustStorePassword 属性指定用来检查 trustStore 数据完整性的密码  。 有关使用 JVM 的默认信任存储区的详细信息，请参阅[为加密配置客户端](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)。  
  
 下面的代码示例演示如何在连接字符串中设置 trustStore 和 trustStorePassword 属性   ：  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC 驱动程序提供了一个附加属性 hostNameInCertificate，该属性指定服务器的主机名  。 此属性的值必须与证书的 subject 属性一致。  
  
 下面的代码示例演示如何在连接字符串中使用 hostNameInCertificate 属性  ：  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  或者，可以使用由 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类提供的适当的资源库方法来设置连接属性的值  。  
  
 在 encrypt 属性设置为 true 且 trustServerCertificate 属性设置为 false 的情况下，如果连接字符串中的服务器名称与 TLS 证书中的服务器名称不符，则会出现以下错误：`The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`     。 从版本 7.2 开始，驱动程序在 TLS 证书的服务器名称最左边的标签中支持通配符模式匹配。

## <a name="see-also"></a>另请参阅

 [使用加密](../../connect/jdbc/using-ssl-encryption.md)[保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)