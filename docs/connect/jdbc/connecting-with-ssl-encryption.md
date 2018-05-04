---
title: 使用 SSL 加密连接 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86bdeaf93e6269294f15d98cbe0f0a0e88f5788b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-ssl-encryption"></a>使用 SSL 加密进行连接
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主题中的示例描述如何使用连接字符串属性允许应用程序在 Java 应用程序中使用安全套接字层 (SSL) 加密。 有关这些新的连接字符串属性如**加密**， **trustServerCertificate**， **trustStore**， **trustStorePassword**，和**hostNameInCertificate**，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 当**加密**属性设置为**true**和**trustServerCertificate**属性设置为**true**、 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将不会验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。 这是通常需要在测试环境中，例如何处允许连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例具有自签名的证书。  
  
 下面的代码示例演示如何设置**trustServerCertificate**连接字符串中的属性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 当**加密**属性设置为**true**和**trustServerCertificate**属性设置为**false**、 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 在通过使用连接时必须验证服务器证书，以便提供信任材料**trustStore**和**trustStorePassword**连接属性显式，或通过使用基础 Java 虚拟机 (JVM) 的默认信任隐式存储。  
  
 **TrustStore**属性到证书信任库文件，其中包含的客户端信任的证书列表中指定的路径 （包括文件名）。 **TrustStorePassword**属性指定用于检查 trustStore 数据的完整性的密码。 有关使用 JVM 的默认信任存储区的详细信息，请参阅[配置 SSL 加密的客户端](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)。  
  
 下面的代码示例演示如何设置**trustStore**和**trustStorePassword**连接字符串中的属性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC 驱动程序提供附加属性， **hostNameInCertificate**，它指定服务器的主机名。 此属性的值必须与证书的 subject 属性一致。  
  
 下面的代码示例演示如何使用**hostNameInCertificate**连接字符串中的属性：  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  或者，可以使用合适的设置连接属性的值**setter**提供方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)类。  
  
 如果**加密**属性设置为**true**和**trustServerCertificate**属性设置为**false**和如果服务器中的名称连接字符串与中的服务器名称不匹配[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书的情况下将发出以下错误： 该驱动程序无法建立安全连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]通过安全套接字层 (SSL) 加密。 错误:“java.security.cert.CertificateException: 在安全套接字层(SSL)初始化过程中验证证书中的服务器名称失败。”  
  
## <a name="see-also"></a>另请参阅  
 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)   
 [保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
