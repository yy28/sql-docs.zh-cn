---
title: "加密连接到 Linux 上的 SQL Server |Microsoft 文档"
description: "本主题介绍在 Linux 上的加密对 SQL Server 的连接。"
author: tmullaney
ms.date: 10/02/2017
ms.author: meetb;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords: Linux, encrypted connections
ms.workload: Inactive
ms.openlocfilehash: f2f0792202d3af6be0e24ff8b24532598c8d0c84
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密连接到 Linux 上的 SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上可以使用传输层安全 (TLS)，客户端应用程序和的实例之间跨网络传输的数据进行加密[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Windows 和 Linux 上支持相同的 TLS 协议： TLS 1.2、 1.1 和 1.0。 但是，若要配置 TLS 的步骤是特定于操作系统在其上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在运行。  

## <a name="requirements-for-certificates"></a>对证书的要求 
我们开始之前，你需要确保你的证书遵循这些要求：
- 当前系统时间必须晚到属性的证书从证书以及有效之前的属性有效。
- 该证书必须用于服务器身份验证。 这要求要指定服务器身份验证 (1.3.6.1.5.5.7.3.1) 的证书的增强型密钥用法属性。
- 必须使用 AT_KEYEXCHANGE KeySpec 选项创建证书。 通常情况下，证书的密钥用法属性 (KEY_USAGE) 还将包括密钥加密 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)。
- 证书的使用者属性必须指示的公用名 (CN) 为主机名或服务器计算机的完全限定的域名 (FQDN) 是相同。 注意： 支持通配符证书。 

## <a name="overview"></a>概述
TLS 用于加密从客户端应用程序的连接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 正确配置时，TLS 会提供隐私和数据完整性，客户端和服务器之间进行通信。  TLS 连接可以是客户端 intiated 或服务器 initited。 


## <a name="client-initiated-encryption"></a>客户端启动的加密 
- **生成证书**（/CN 应匹配你的 SQL Server 主机完全限定域名名）

> [!NOTE]
> 对于此示例，我们使用自签名的证书，这应不用于生产方案。 你应使用 CA 证书。 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **将 SQL Server 配置**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **注册客户端计算机 （Windows、 Linux 或 macOS） 上的证书**

    -   如果您正在使用需要复制到客户端计算机上而不是用户证书的证书颁发机构 (CA) 证书的 CA 签名的证书。 
    -   如果你只需使用的自签名的证书的.pem 文件复制到分发到相应的以下文件夹并执行命令以启用它们 
        - **Ubuntu** ： 将证书复制到```/usr/share/ca-certificates/```.crt 重命名扩展使用 dpkg reconfigure ca 证书，使它作为系统 CA 证书。 
        - **RHEL** ： 将证书复制到```/etc/pki/ca-trust/source/anchors/```使用```update-ca-trust```，使它作为系统 CA 证书。
        - **SUSE** ： 将证书复制到```/usr/share/pki/trust/anchors/```使用```update-ca-certificates```以便就系统 CA 证书。
        - **Windows**： 导入为下当前用户证书的.pem 文件-> 受信任根证书颁发机构证书->
        - **macOS**: 
           - 将复制到证书```/usr/local/etc/openssl/certs```
           - 运行以下命令来获取的哈希值：```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - 将 cert 重命名为值。 例如： ```mv mssql.pem dc2dd900.0```。 请确保 dc2dd900.0 处于```/usr/local/etc/openssl/certs```
    
-   **连接字符串示例** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS 连接对话框](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 连接对话框")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>由服务器启动的加密 

- **生成证书**（/CN 应匹配你的 SQL Server 主机完全限定域名名）
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **将 SQL Server 配置**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **连接字符串示例** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> 设置**TrustServerCertificate**为 True，如果客户端无法连接到 CA，以验证该证书的真实性

## <a name="common-connection-errors"></a>常见的连接错误  

|错误消息 |Fix |
|--- |--- |
|由不受信任的颁发机构颁发的证书链。  |当客户端无法验证 SQL Server 在 TLS 握手期间提供的证书上的签名时，将出现此错误。 请确保客户端信任是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]直接，证书或签名的 SQL Server 证书的 CA。 |
|目标主体名称不正确。  |请确保 SQL 服务器的证书上的公用名字段与客户端的连接字符串中指定的服务器名称匹配。 |  
|现有的连接被远程主机强行关闭。 |当客户端不支持所需的 SQL Server 的 TLS 协议版本，可以出现此错误。 例如，如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]配置为要求使用 TLS 1.2，请确保你的客户端还支持 TLS 1.2 协议。 |
| | |   
