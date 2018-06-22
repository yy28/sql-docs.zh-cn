---
title: 使用未经验证的加密 |Microsoft 文档
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f8be993a5f06a5d76021755e6dca8b2544616d4b
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696768"
---
# <a name="using-encryption-without-validation"></a>使用不带验证的加密
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终对与登录相关的网络数据包进行加密。 如果在服务器启动时未为其提供任何证书，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将生成可用于对登录数据包进行加密的自签名证书。  

自签名的证书不会保证安全。 加密的握手基于 NT LAN Manager (NTLM)。 强烈建议你预配 SQL Server 上的安全连接可验证的证书。 传输安全层 (TLS) 可以进行安全只能使用证书验证。

应用程序还可以通过使用连接字符串关键字或连接属性请求对所有网络流量加密。 关键字是用于 ODBC 和 OLE DB 的"加密"时使用的提供程序字符串**idbinitialize:: Initialize**，或"使用加密数据的"适用于 ADO 和 OLE DB 使用带有的初始化字符串时**IDataInitialize**. 这也可能配置的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 使用**强制协议加密**选项，然后通过配置客户端请求加密的连接。 默认情况下，对某一连接的所有网络流量加密要求在服务器上设置证书。 通过设置你的客户端信任的服务器上的证书，你可能会变得容易遭受拦截的攻击。 如果部署在服务器上可验证的证书，请确保将有关信任证书的客户端设置更改为 FALSE。

有关连接字符串关键字的信息，请参阅[Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 若要启用加密时尚未在服务器上，设置证书用于[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 可以用于同时设置**强制协议加密**和**信任服务器证书**选项。 在这种情况下，如果服务器上未设置可验证的证书，加密将使用不带验证的自签名服务器证书。  
  
 应用程序还可以使用 "TrustServerCertificate" 关键字或与其关联的连接属性确保执行加密。 应用程序设置从不会降低 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置管理器设置的安全级别，相反还可能提高安全级别。 例如，如果**强制协议加密**未设置的客户端应用程序可能会请求本身的加密。 甚至是在未设置服务器证书的情况下，为保证加密，应用程序也可能请求加密和 "TrustServerCertificate"。 不过，如果在客户端配置中未启用 "TrustServerCertificate"，则仍需要已设置的服务器证书。 下表介绍了各种情况：  
  
|“强制协议加密”客户端设置|“信任服务器证书”客户端设置|连接字符串/连接属性加密/对数据使用加密|连接字符串/连接属性信任服务器证书|结果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|“否”|N/A|否（默认值）|忽略|无加密。|  
|“否”|N/A|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|“否”|N/A|是|是|始终加密，但可能使用自签名的服务器证书。|  
|是|“否”|忽略|忽略|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|否（默认值）|忽略|始终加密，但可能使用自签名的服务器证书。|  
|是|是|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|是|是|加密始终发生，但可能使用的自签名的服务器证书。|  
||||||

> [!CAUTION]
> 上表仅在不同配置的系统行为上提供的指南。 对于安全的连接，请确保客户端和服务器都需要进行加密。 另外，请确保服务器具有可验证的证书，并且**TrustServerCertificate**上客户端设置设置为 FALSE。

## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持且无需通过 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 数据源初始化属性，用于实现 dbpropset_sqlserverdbinit 限属性中添加验证的加密设置。 此外，新的连接字符串关键字，"TrustServerCertificate"，如已添加。 它接受是或否值;不是默认设置。 使用服务组件时，它接受值 true 或 false；默认值为 false。  
  
 有关 dbpropset_sqlserverdbinit 限属性集对所做的增强功能的详细信息，请参阅[初始化和授权属性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持且无需通过添加验证的加密[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函数。 添加了 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 以接受 SQL_TRUST_SERVER_CERTIFICATE_YES 或 SQL_TRUST_SERVER_CERTIFICATE_NO，默认值为 SQL_TRUST_SERVER_CERTIFICATE_NO。 此外，还添加了新的连接字符串关键字 "TrustServerCertificate"。 它接受值 yes 或 no；默认值为 no。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
