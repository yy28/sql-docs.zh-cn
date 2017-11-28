---
title: "连接字符串关键字和数据源名称 (Dsn) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: "41"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2020ce16f722354b49a7e35e4a3f1e1706b6a2d5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="connection-string-keywords-and-data-source-names-dsns"></a>连接字符串关键字和数据源名称 (DSN)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题讨论如何创建连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。  
  
## <a name="connection-properties"></a>连接属性  
对于此版本的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 或 macOS 上，你可以使用以下连接关键字：  
  
||||||  
|-|-|-|-|-|  
|`Addr`|`Address`|`ApplicationIntent`|`AutoTranslate`|`Database`|
|`Driver`|`DSN`|`Encrypt`|`FileDSN`|`MARS_Connection`|  
|`MultiSubnetFailover`|`PWD`|`Server`|`Trusted_Connection`|`TrustServerCertificate`|  
|`UID`|`WSID`|`ColumnEncryption`|`TransparentNetworkIPResolution`||  

> [!IMPORTANT]  
> 当连接到使用数据库镜像（有一个故障转移伙伴）的数据库时，不要在连接字符串中指定数据库名称。 相反，发送**使用** *database_name*命令以在执行查询之前连接到数据库。  
  
有关这些关键字的详细信息，请参阅 [将连接字符串关键字用于 SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkID=126696)的 ODBC 部分。  
  
传递给值**驱动程序**关键字可以是以下之一：  
  
-   安装该驱动程序时使用的名称。

-   驱动程序库，后者在用来安装驱动程序的模板.ini 文件中指定路径。  

若要创建 DSN，创建 （如有必要） 并编辑文件**~/.odbc.ini** (`.odbc.ini`主目录中) 为仅供当前用户，用户 DSN 或`/etc/odbc.ini`的系统 DSN （管理所需特权。）下面是一个示例文件，DSN 显示最小所需的项：  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

你可以选择指定协议和端口来连接到服务器。 例如， **Server = tcp:***servername***、 12345**。 请注意，唯一支持的 Linux 和 macOS 驱动程序的协议是`tcp`。

若要连接到静态端口上的命名实例，使用<b>Server =</b>*servername*，**port_number**。 不支持连接到的动态端口。  

或者，您可以将 DSN 信息添加到一个模板文件，并执行以下命令以将其添加到`~/.odbc.ini`:
 - **odbcinst-i-s-f** *template_file*  
 
你可以验证您的驱动程序正在使用`isql`若要测试该连接，也可以使用此命令：
 - **bcp master.INFORMATION_SCHEMA.TABLES 出 OutFile.dat-S <server> -U <name> -P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>使用安全套接字层 (SSL)  
你可以使用安全套接字层 (SSL) 加密连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 SSL 保护[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]用户名和密码通过网络。 SSL 还会验证服务器的标识以抵御中间人 (MITM) 攻击。  

启用加密可提高安全性，但会降低性能。

有关详细信息，请参阅[加密对 SQL Server 的连接](http://go.microsoft.com/fwlink/?LinkId=220900)和[使用未经验证的加密](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)。

无论 **Encrypt** 和 **TrustServerCertificate**的设置如何，服务器登录凭据（用户名和密码）都始终处于加密状态。 下表显示了 **Encrypt** 和 **TrustServerCertificate** 设置的效果。  

||**TrustServerCertificate = 否**|**TrustServerCertificate = yes**|  
|-|-------------------------------------|------------------------------------|  
|**加密 = 否**|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据没有加密。|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据没有加密。|  
|**加密 = yes**|检查服务器证书。<br /><br />在客户端和服务器之间发送的数据已加密。<br /><br />在使用者公用名 (CN) 或使用者备用名称 (SAN) 中的名称 （或 IP 地址） [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 证书应与连接字符串中指定的服务器名称 （或 IP 地址） 完全匹配。|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据已加密。|  

默认情况下，加密的连接会始终验证服务器的证书。 但是，如果你连接到了自签名的证书的服务器，还添加`TrustServerCertificate`绕过检查的针对受信任的证书颁发机构的列表的证书的选项：  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL 使用 OpenSSL 库。 下表显示了 OpenSSL 的受支持的最低版本和每个平台的默认证书信任存储位置：

|平台|最低的 OpenSSL 版本|默认证书信任存储位置|  
|------------|---------------------------|--------------------------------------------|
|Debian 8.71 |1.0.1t|/etc/ssl/certs|
|macOS 10.12|1.0.2k|/usr/local/etc/openssl/certs|
|OS X 10.11|1.0.2j|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|  
|Red Hat Enterprise Linux 7|1.0.1e|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1i|/etc/ssl/certs|
|Ubuntu 15.10 |1.0.2d|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2g|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2g|/etc/ssl/certs|
  
你还可以指定在连接字符串中使用加密`Encrypt`选项时使用**SQLDriverConnect**连接。

## <a name="see-also"></a>另请参阅  
[安装 Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
