---
title: 加密连接到 Linux 上的 SQL Server |Microsoft Docs
description: 本文介绍在 Linux 上的加密与 SQL Server 的连接。
author: tmullaney
ms.date: 01/30/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: f7b1dd57af300fc3e3fa61e469646211536b4653
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001819"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>加密连接到 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 Linux 上可以使用传输层安全性 (TLS) 通过客户端应用程序和实例之间的网络传输的数据进行加密[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持 Windows 和 Linux 上使用相同的 TLS 协议： TLS 1.2、 1.1 和 1.0。 但是，若要配置 TLS 的步骤是特定于其上的操作系统[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在运行。  

## <a name="requirements-for-certificates"></a>对证书的要求 
开始之前，您需要确保你的证书符合以下要求：
- 当前系统时间必须晚于证书的属性从属性，该证书并有效之前有效。
- 该证书必须用于服务器身份验证。 这要求指定服务器身份验证 (1.3.6.1.5.5.7.3.1) 的证书的增强型密钥用法属性。
- 通过使用 AT_KEYEXCHANGE KeySpec 选项，必须创建该证书。 通常情况下，证书的密钥用法属性 (KEY_USAGE) 还包括密钥加密 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)。
- 证书的 Subject 属性必须指明公用名 (CN) 为主机名或服务器计算机的完全限定的域名 (FQDN) 是相同。 注意： 支持通配符证书。 

## <a name="overview"></a>概述
TLS 用于加密从客户端应用程序的连接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 正确配置时，TLS 提供隐私和数据完整性的客户端和服务器之间的通信。  TLS 连接可以是启动的客户端或服务器启动。 


## <a name="client-initiated-encryption"></a>客户端启动的加密 
- **生成证书**（/CN 应在 SQL Server 完全限定的域名与主机名匹配）

> [!NOTE]
> 对于此示例，我们使用自签名证书，这应不用于生产方案。 应使用 CA 证书。 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **配置 SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **注册客户端计算机 （Windows、 Linux 或 macOS） 上的证书**

    -   如果使用 CA 签名的证书，你必须复制到客户端计算机上而不是用户证书的证书颁发机构 (CA) 证书。 
    -   如果使用自签名的证书，只需将.pem 文件复制到分发到相应的以下文件夹并执行命令来启用它们 
        - **Ubuntu**： 将证书复制到```/usr/share/ca-certificates/```重命名为.crt 的扩展插件使用 dpkg 重新配置 ca 证书，使它作为系统 CA 证书。 
        - **RHEL**： 将证书复制到```/etc/pki/ca-trust/source/anchors/```使用```update-ca-trust```，使它作为系统 CA 证书。
        - **SUSE**： 将证书复制到```/usr/share/pki/trust/anchors/```使用```update-ca-certificates```，使它作为系统 CA 证书。
        - **Windows**： 作为当前用户下的证书的.pem 文件-> 导入受信任的根证书颁发机构证书->
        - **macOS**: 
           - 将复制到证书 ```/usr/local/etc/openssl/certs```
           - 运行以下命令以获取哈希值： ```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - 重命名为值的证书。 例如： ```mv mssql.pem dc2dd900.0```。 请确保在 dc2dd900.0 ```/usr/local/etc/openssl/certs```
    
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

- **配置 SQL Server**

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
> 设置**TrustServerCertificate**为 true; 如果客户端无法连接到用于验证证书的真实性的 CA

## <a name="common-connection-errors"></a>常见的连接错误  

|错误消息 |Fix |
|--- |--- |
|由不受信任的颁发机构颁发的证书链。  |当客户端将无法验证 SQL Server 在 TLS 握手期间提供的证书上签名时，将发生此错误。 请确保客户端信任是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]直接，证书或 CA 签名的 SQL Server 证书。 |
|目标主体名称不正确。  |请确保 SQL Server 的证书公用名称字段匹配客户端的连接字符串中指定的服务器名称。 |  
|现有连接被远程主机强行关闭。 |客户端不支持所需的 SQL Server 的 TLS 协议版本时，可能发生此错误。 例如，如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]配置为需要 TLS 1.2，请确保你的客户端还支持 TLS 1.2 协议。 |
| | |   
