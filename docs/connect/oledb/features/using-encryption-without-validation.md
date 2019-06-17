---
title: 使用不带验证的加密 |Microsoft Docs
description: 使用不带验证的加密
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 108aef449d80fa01e88fac29e6058754626b6aed
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802884"
---
# <a name="using-encryption-without-validation"></a>使用不带验证的加密
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终对与登录相关的网络数据包进行加密。 如果在服务器启动时未为其提供任何证书，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将生成可用于对登录数据包进行加密的自签名证书。  

自签名的证书并不保证安全。 加密的握手基于 NT LAN Manager (NTLM)。 强烈建议预配 SQL Server 上的安全连接性可验证的证书。 传输安全层 (TLS) 可以进行安全仅使用证书验证。

应用程序还可以通过使用连接字符串关键字或连接属性请求对所有网络流量加密。 将访问接口字符串用于 IDbInitialize::Initialize 时，OLE DB 中的关键字为“Encrypt”；将初始化字符串用于 IDataInitialize 时，ADO 和 OLE DB 中的关键字为“Use Encryption for Data”   。 这也可以通过配置[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 Configuration Manager**强制协议加密**选项，并通过配置客户端为请求加密的连接。 默认情况下，对某一连接的所有网络流量加密要求在服务器上设置证书。 通过设置你的客户端信任的服务器上的证书，你可能会变得很容易受到人为干预攻击。 如果部署服务器上的可验证证书，请确保将信任该证书有关的客户端设置更改为 FALSE。

有关连接字符串关键字的信息，请参阅[将连接字符串关键字用于适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md )。  
  
 若要在服务器上未设置证书时启用加密，可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器设置“强制协议加密”和“信任服务器证书”选项   。 在这种情况下，如果服务器上未设置可验证的证书，加密将使用不带验证的自签名服务器证书。  
  
 应用程序还可以使用 "TrustServerCertificate" 关键字或与其关联的连接属性确保执行加密。 应用程序设置从不会降低 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置管理器设置的安全级别，相反还可能提高安全级别。 例如，如果没有为客户端设置“强制协议加密”，应用程序可能自行请求加密  。 甚至是在未设置服务器证书的情况下，为保证加密，应用程序也可能请求加密和 "TrustServerCertificate"。 不过，如果在客户端配置中未启用 "TrustServerCertificate"，则仍需要已设置的服务器证书。 下表介绍了各种情况：  
  
|“强制协议加密”客户端设置|“信任服务器证书”客户端设置|连接字符串/连接属性加密/对数据使用加密|连接字符串/连接属性信任服务器证书|结果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|N/A|否（默认值）|忽略|无加密。|  
|否|N/A|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|否|N/A|是|是|始终加密，但可能使用自签名的服务器证书。|  
|是|否|忽略|忽略|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|否（默认值）|忽略|始终加密，但可能使用自签名的服务器证书。|  
|是|是|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|是|是|始终加密，但可能使用自签名的服务器证书。|  
||||||

> [!CAUTION]
> 上表仅在不同配置下的系统行为提供的指南。 安全连接，请确保客户端和服务器都需要加密。 此外请确保服务器具有可验证的证书，并且**TrustServerCertificate**上客户端设置设置为 FALSE。

## <a name="ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序 
 适用于 SQL Server 的 OLE DB 驱动程序通过添加 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 数据源初始化属性（在 DBPROPSET_SQLSERVERDBINIT 属性集中实现）支持不带验证的加密。 此外，还添加了新的连接字符串关键字“TrustServerCertificate”。 它接受值 yes 或 no；默认值为 no。 使用服务组件时，它接受值 true 或 false；默认值为 false。  
  
 有关 DBPROPSET_SQLSERVERDBINIT 属性集对所做的增强功能的详细信息，请参阅[初始化和授权属性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  

  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
