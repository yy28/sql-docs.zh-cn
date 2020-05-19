---
title: 使用不带验证的加密 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e1fbea13b0ad9744e1cbe6240c9084f8fda6dc2e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704307"
---
# <a name="using-encryption-without-validation"></a>使用不带验证的加密
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 始终对与登录相关的网络数据包进行加密。 如果在服务器启动时未为其提供任何证书，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将生成可用于对登录数据包进行加密的自签名证书。  
  
 应用程序还可以通过使用连接字符串关键字或连接属性请求对所有网络流量加密。 当使用包含**IDbInitialize：： Initialize**的提供程序字符串或在 OLE DB 将初始化字符串与**IDataInitialize**结合使用时，这些关键字对 ODBC 和 OLE DB 使用提供程序字符串。 这还可以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 "**强制协议加密**" 选项 Configuration Manager 进行配置。 默认情况下，对某一连接的所有网络流量加密要求在服务器上设置证书。  
  
 有关连接字符串关键字的详细信息，请参阅将[连接字符串关键字用于 SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 若要在服务器上未设置证书时启用加密，可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器设置“强制协议加密”和“信任服务器证书”选项********。 在这种情况下，如果服务器上未设置可验证的证书，加密将使用不带验证的自签名服务器证书。  
  
 应用程序还可以使用 "TrustServerCertificate" 关键字或与其关联的连接属性确保执行加密。 应用程序设置从不会降低 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置管理器设置的安全级别，相反还可能提高安全级别。 例如，如果没有为客户端设置“强制协议加密”，应用程序可能自行请求加密****。 甚至是在未设置服务器证书的情况下，为保证加密，应用程序也可能请求加密和 "TrustServerCertificate"。 不过，如果在客户端配置中未启用 "TrustServerCertificate"，则仍需要已设置的服务器证书。 下表介绍了各种情况：  
  
|“强制协议加密”客户端设置|“信任服务器证书”客户端设置|连接字符串/连接属性加密/对数据使用加密|连接字符串/连接属性信任服务器证书|结果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|空值|否（默认值）|忽略|无加密。|  
|否|空值|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|否|空值|是|是|始终加密，但可能使用自签名的服务器证书。|  
|是|否|忽略|忽略|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|否（默认值）|忽略|始终加密，但可能使用自签名的服务器证书。|  
|是|是|是|否（默认值）|仅当存在可验证的服务器证书时才加密，否则连接尝试将失败。|  
|是|是|是|是|始终加密，但可能使用自签名的服务器证书。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序通过添加 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 数据源初始化属性（在 DBPROPSET_SQLSERVERDBINIT 属性集中实现）来支持未经验证的加密。 此外，还添加了新的连接字符串关键字“TrustServerCertificate”。 它接受值 yes 或 no；默认值为 no。 使用服务组件时，它接受值 true 或 false；默认值为 false。  
  
 若要详细了解 DBPROPSET_SQLSERVERDBINIT 属性集的增强，请参阅[初始化和授权属性](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序通过向[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)函数添加内容来支持未经验证的加密。 添加了 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 以接受 SQL_TRUST_SERVER_CERTIFICATE_YES 或 SQL_TRUST_SERVER_CERTIFICATE_NO，默认值为 SQL_TRUST_SERVER_CERTIFICATE_NO。 此外，还添加了新的连接字符串关键字 "TrustServerCertificate"。 它接受值 yes 或 no；默认值为 no。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
