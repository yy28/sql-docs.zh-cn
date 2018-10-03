---
title: 应用程序安全性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42cf0e2a39a4a08ceab94e5391d3c926fb5751ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775755"
---
# <a name="application-security"></a>应用程序安全性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，必须采取预防措施确保应用程序的安全性。 可以采取一些步骤来帮助保护应用程序，下列部分提供了有关这一方面的信息。  
  
## <a name="using-java-policy-permissions"></a>使用 Java 策略权限  
 使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 时，必须指定 JDBC 驱动程序所要求的 Java 策略权限。 Java 运行时环境 (JRE) 提供了一个可在运行时使用的大型安全模型，用于确定线程是否具有对资源的访问权限。 安全策略文件可控制该访问权限。 策略文件本身由部署者和容器的系统管理员管理，但该主题所列出的权限会影响 JDBC 驱动程序的正常运行。  
  
 策略文件中典型的权限如下所示：  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 以下代码库应限制为 JDBC 驱动程序代码库，以确保授予最少数量的特权。  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  代码“file:/install_dir/lib/-”是指 JDBC 驱动程序的安装目录。  
  
## <a name="protecting-server-communication"></a>保护服务器通信  
 使用 JDBC 驱动程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库进行通信时，可以使用 Internet 协议安全 (IPSEC) 和/或安全套接字层 (SSL) 来保护信道。  
  
 SSL 支持可用于在 IPSEC 保护措施之外提供另一层保护。 有关使用 SSL 的详细信息，请参阅[Using SSL Encryption](../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另请参阅  
 [保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
