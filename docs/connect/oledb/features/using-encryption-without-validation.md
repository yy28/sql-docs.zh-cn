---
title: 使用未经验证的加密 |Microsoft 文档
description: 使用未经验证的加密
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be4885de83c5d189b1772c6fe04eff1a744cafef
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="using-encryption-without-validation"></a>使用不带验证的加密
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终对与登录相关的网络数据包进行加密。 如果在服务器启动时未为其提供任何证书，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将生成可用于对登录数据包进行加密的自签名证书。  

自签名的证书不会保证安全。 加密的握手基于 NT LAN Manager (NTLM)。 强烈建议你预配 SQL Server 上的安全连接可验证的证书。 传输安全层 (TLS) 可以进行安全只能使用证书验证。

应用程序还可以通过使用连接字符串关键字或连接属性请求对所有网络流量加密。 关键字是用于 OLE DB 的"加密"时使用的提供程序字符串**idbinitialize:: Initialize**，或"使用加密数据的"适用于 ADO 和 OLE DB 使用带有的初始化字符串时**IDataInitialize**. 这也可能配置的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 使用**强制协议加密**选项，然后通过配置客户端请求加密的连接。 默认情况下，对某一连接的所有网络流量加密要求在服务器上设置证书。 通过设置你的客户端信任的服务器上的证书，你可能会变得容易遭受拦截的攻击。 如果部署在服务器上可验证的证书，请确保将有关信任证书的客户端设置更改为 FALSE。

有关连接字符串关键字的信息，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md )。  
  
 若要启用加密时尚未在服务器上，设置证书用于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 可以用于同时设置**强制协议加密**和**信任服务器证书**选项。 在这种情况下，如果服务器上未设置可验证的证书，加密将使用不带验证的自签名服务器证书。  
  
 应用程序还可以使用 "TrustServerCertificate" 关键字或与其关联的连接属性确保执行加密。 应用程序设置从不会降低 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置管理器设置的安全级别，相反还可能提高安全级别。 例如，如果**强制协议加密**未设置的客户端应用程序可能会请求本身的加密。 甚至是在未设置服务器证书的情况下，为保证加密，应用程序也可能请求加密和 "TrustServerCertificate"。 不过，如果在客户端配置中未启用 "TrustServerCertificate"，则仍需要已设置的服务器证书。 下表介绍了各种情况：  
  
|“强制协议加密”客户端设置|“信任服务器证书”客户端设置|连接字符串/连接属性加密/对数据使用加密|连接字符串/连接属性信任服务器证书|结果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|N/A|否（默认值）|忽略|无加密。|  
|否|N/A|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|否|N/A|是|是|始终加密，但可能使用自签名的服务器证书。|  
|是|否|忽略|忽略|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|否（默认值）|忽略|始终加密，但可能使用自签名的服务器证书。|  
|是|用户帐户控制|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|用户帐户控制|用户帐户控制|是|加密始终发生，但可能使用的自签名的服务器证书。|  
||||||

> [!CAUTION]
> 上表仅在不同配置的系统行为上提供的指南。 对于安全的连接，请确保客户端和服务器都需要进行加密。 另外，请确保服务器具有可验证的证书，并且**TrustServerCertificate**上客户端设置设置为 FALSE。

## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序 
 SQL Server 的 OLE DB 驱动程序支持在不验证 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 数据源初始化属性，用于实现 dbpropset_sqlserverdbinit 限设置的属性中添加了加密。 此外，新的连接字符串关键字，"TrustServerCertificate"，如已添加。 它接受是或否值;不是默认设置。 使用服务组件时，它接受值 true 或 false；默认值为 false。  
  
 有关 dbpropset_sqlserverdbinit 限属性集对所做的增强功能的详细信息，请参阅[初始化和授权属性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  

  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
