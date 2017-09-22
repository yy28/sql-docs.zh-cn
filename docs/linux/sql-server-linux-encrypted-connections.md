---
title: "加密连接到 Linux 上的 SQL Server |Microsoft 文档"
description: "本主题介绍在 Linux 上的加密对 SQL Server 的连接。"
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 47a15701730019aaf166743c47c606aa2059b7fe
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密连接到 Linux 上的 SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上可以使用传输层安全 (TLS)，客户端应用程序和的实例之间跨网络传输的数据进行加密[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Windows 和 Linux 上支持相同的 TLS 协议： TLS 1.2、 1.1 和 1.0。 但是，若要配置 TLS 的步骤是特定于操作系统在其上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在运行。  
 
## <a name="typical-scenario"></a>典型方案 
TLS 用于加密从客户端应用程序的连接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 正确配置时，TLS 会提供隐私和数据完整性，客户端和服务器之间进行通信。  
以下步骤介绍典型的方案：  

1. 数据库管理员生成私钥和证书签名请求 (CSR)。 CSR 的公用名应与客户端在其 SQL Server 连接字符串中指定的服务器名称匹配。 此公用名通常是的完全限定的域名称[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机。 若要为多个服务器使用相同的证书，你可以在公用名使用通配符 (例如，`"*.contoso.com"`而不是`"node1.contoso.com"`)。   
2. CSR 发送到的证书颁发机构 (CA) 签名。 CA 应连接到的所有客户端计算机受信任[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 CA 的数据库管理员返回签名的证书。   
3. 数据库管理员配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]要私钥和签名的证书用于 TLS 连接。   
4. 客户端指定`"Encrypt=True"`和`"TrustServerCertificate=False"`其连接字符串中。 （特定的参数名称可能不同，具体取决于正在使用哪个驱动程序）。 客户端现在尝试加密到 SQL Server 的连接，并检查 SQL Server 的证书，以防止在拦截攻击的有效性。  
 
## <a name="configuring-tls-on-linux"></a>在 Linux 上配置 TLS  

使用`mssql-conf`的实例配置 TLS[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上运行。 支持以下选项：  

|选项 |Description |
|--- |--- |
|`network.forceencryption` |如果为 1，然后[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]强制所有连接进行加密。 默认情况下，此选项为 0。 |  
|`network.tlscert` |证书的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用于 TLS。 示例：`/etc/ssl/certs/mssql.pem`证书文件必须是可由 mssql 帐户访问。 Microsoft 建议限制访问文件使用`chown mssql:mssql <file>; chmod 400 <file>`。 |  
|`network.tlskey` |私钥的绝对路径文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用于 TLS。 示例：`/etc/ssl/private/mssql.key`证书文件必须是可由 mssql 帐户访问。 Microsoft 建议限制访问文件使用`chown mssql:mssql <file>; chmod 400 <file>`。 | 
|`network.tlsprotocols` |哪些 TLS 协议都允许 SQL Server 的逗号分隔的列表。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]始终尝试协商允许的最高协议。 如果客户端不支持任何允许的协议，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]拒绝连接尝试。  为了实现兼容，默认情况下，（1.2、 1.1、 1.0） 允许所有支持的协议。  如果你的客户端支持 TLS 1.2，Microsoft 建议允许仅 TLS 1.2。 |  
|`network.tlsciphers` |指定允许哪些密码[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tls。 此字符串的格式必须设置每个[OpenSSL 的密码的列表格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情况下，你应该不需要更改此选项。 <br /> 默认情况下，允许以下密码： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>示例 
此示例使用自签名的证书。 在正常生产方案中，将通过所有客户端信任的 CA 签名证书。  
 
### <a name="step-1-generate-private-key-and-certificate"></a>步骤 1： 生成私钥和证书 
打开命令在 Linux 计算机上的终端其中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在运行。 运行以下命令：  

- 生成自签名的证书。 请确保 /CN 匹配你的 SQL Server 主机完全限定域名名。 （可选） 可以使用通配符，例如`'/CN=*.contoso.com'`。    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- 限制对的访问`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 600 mssql.pem mssql.key 
   ```  
 
- 将移动到系统 SSL 目录 （可选）  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversionincludesssnoversion-mdmd"></a>步骤 2： 配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
使用`mssql-conf`配置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]若要使用的证书和密钥，以 TLS。 为了提高安全性，还可以将 TLS 1.2 设置为唯一允许协议并强制所有客户端使用加密的连接。  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversionincludesssnoversion-mdmd"></a>步骤 3： 重新启动[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]必须重新启动这些更改才会生效。  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>步骤 4： 将自签名的证书复制到客户端计算机 
由于本示例使用由自签名证书[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主机，必须复制证书 （不是私钥），并将其连接到的所有客户端计算机上的受信任的根证书作为安装[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果该证书由所有客户端已信任的 CA 签名的则不需要此步骤。 
 
### <a name="step-5-connect-from-clients-using-tls"></a>从客户端使用 TLS 连接的步骤 5: 
连接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]从客户端同时启用加密和`TrustServerCertificate`设置为`False`连接字符串中。 下面是如何指定这些参数使用不同的工具和驱动程序的几个示例。 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]   
  ![SSMS 连接对话框](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 连接对话框")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>常见的连接错误  

|错误消息 |Fix |
|--- |--- |
|由不受信任的颁发机构颁发的证书链。  |当客户端无法验证 SQL Server 在 TLS 握手期间提供的证书上的签名时，将出现此错误。 请确保客户端信任是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]直接，证书或签名的 SQL Server 证书的 CA。 |
|目标主体名称不正确。  |请确保 SQL 服务器的证书上的公用名字段与客户端的连接字符串中指定的服务器名称匹配。 |  
|现有的连接被远程主机强行关闭。 |当客户端不支持所需的 SQL Server 的 TLS 协议版本，可以出现此错误。 例如，如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]配置为要求使用 TLS 1.2，请确保你的客户端还支持 TLS 1.2 协议。 |
| | |   


