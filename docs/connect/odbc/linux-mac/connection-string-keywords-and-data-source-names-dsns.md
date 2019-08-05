---
title: 连接到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702807"
---
# <a name="connecting-to-sql-server"></a>连接到 SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本主题讨论如何创建与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的连接。  
  
## <a name="connection-properties"></a>连接属性  

有关 Linux 和 Mac 上支持的所有连接字符串关键字和属性, 请参阅[DSN 和连接字符串关键字和属性](../../../connect/odbc/dsn-connection-string-attribute.md)

> [!IMPORTANT]  
> 当连接到使用数据库镜像（有一个故障转移伙伴）的数据库时，不要在连接字符串中指定数据库名称。 应发送 use database_name 命令连接到该数据库，然后再执行查询   。  
  
传递给**Driver**关键字的值可以是下列值之一:  
  
-   安装该驱动程序时使用的名称。

-   已在用于安装驱动程序的模板 .ini 文件中指定的该驱动程序库的路径。  

若要创建 dsn, 请创建 (如有必要) 并编辑文件 **~/.odbc.ini** (`.odbc.ini`在主目录中), 以使用户 DSN 只能供当前用户或`/etc/odbc.ini`系统 dsn (需要管理权限) 使用。以下示例文件显示了 DSN 所需的条目：  

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

你可以选择指定协议和端口来连接到服务器。 例如, **Server = tcp:** _servername_ **, 12345**。 请注意, Linux 和 macOS 驱动程序支持的唯一协议是`tcp`。

若要连接到静态端口上的命名实例，请使用 Server=servername,port_number<b></b>   。 在 17.4 版之前，不支持连接到动态端口。

可以选择将 DSN 信息添加到模板文件并执行以下命令，以将其添加到 `~/.odbc.ini`：
 - **odbcinst -i -s -f** _template_file_  
 
您可以使用`isql`测试连接来验证您的驱动程序是否正常运行, 也可以使用以下命令:
 - **bcp INFORMATION_SCHEMA 输出的输出数据-S <server> -U <name> -P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>使用安全套接字层 (SSL)  
可以使用安全套接字层 (SSL) 加密与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的连接。 SSL 通过网络保护 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用户名和密码。 SSL 还会验证服务器的标识以抵御中间人 (MITM) 攻击。  

启用加密可提高安全性，但会降低性能。

有关详细信息, 请参阅[加密连接 SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900)和[使用未验证的加密](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)。

无论 **Encrypt** 和 **TrustServerCertificate**的设置如何，服务器登录凭据（用户名和密码）都始终处于加密状态。 下表显示了 **Encrypt** 和 **TrustServerCertificate** 设置的效果。  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据没有加密。|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据没有加密。|  
|**Encrypt=yes**|检查服务器证书。<br /><br />在客户端和服务器之间发送的数据已加密。<br /><br />[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书中使用者公用名 (CN) 或使用者可选名称 (SAN) 中的名称（或 IP 地址）应与连接字符串中指定的服务器名称（或 IP 地址）完全匹配。|不检查服务器证书。<br /><br />在客户端和服务器之间发送的数据已加密。|  

默认情况下，加密的连接会始终验证服务器的证书。 但是, 如果你连接到具有自签名证书的服务器, 还可以添加选项 " `TrustServerCertificate`对受信任的证书颁发机构列表绕过证书":  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL 使用 OpenSSL 库。 下表显示了 OpenSSL 的受支持的最低版本和每个平台的默认证书信任存储位置：

|平台|最低的 OpenSSL 版本|默认证书信任存储位置|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11、macOS 10.12、10.13、10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11、12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10、19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04、16.10、17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

你还可以在使用`Encrypt` **SQLDriverConnect**进行连接时使用选项在连接字符串中指定加密。

## <a name="adjusting-the-tcp-keep-alive-settings"></a>调整 TCP Keep-alive 设置

从 ODBC 驱动程序17.4 开始, 驱动程序发送保持活动状态的数据包并在未收到响应时对它们进行重新传输的频率是可配置的。
若要配置, 请将以下设置添加到中`odbcinst.ini`的驱动程序部分, 或添加到中`odbc.ini`的 DSN 部分。 使用 DSN 进行连接时, 驱动程序将使用 DSN 的部分中的设置 (如果有);否则, 或者, 如果只使用连接字符串进行连接, 它将使用的驱动程序部分中`odbcinst.ini`的设置。 如果这两个位置中不存在该设置, 则驱动程序将使用默认值。

- `KeepAlive=<integer>`控制 TCP 通过发送 keep-alive 数据包来尝试验证空闲连接是否仍保持不变的频率。 默认值为 30 秒  。

- `KeepAliveInterval=<integer>`确定在收到响应之前分隔保持活动传输的时间间隔。  默认值为 **1** 秒。


## <a name="see-also"></a>另请参阅  
[在 Linux 和 macOS 上安装 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)
