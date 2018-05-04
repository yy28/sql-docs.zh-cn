---
title: 了解 SSL 支持 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12d7d92bd86cfd5851715c839f8772d4bc7ae94a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-ssl-support"></a>了解 SSL 支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  连接到时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，如果应用程序请求加密和实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置为支持 SSL 加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]启动 SSL 握手。 握手允许服务器和客户端协商将用于保护数据的加密方式和加密算法。 在完成 SSL 握手之后，客户端和服务器可以安全地发送已加密的数据。 SSL 握手期间服务器向客户端发送其公钥证书。 公钥证书的颁发者称为证书颁发机构 (CA)。 客户端负责验证证书颁发机构是否为客户端信任的证书颁发机构。  
  
 如果应用程序不会请求加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不会强制[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]若要支持 SSL 加密。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例未配置为强制 SSL 加密，但未加密建立的连接。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例配置为强制 SSL 加密、 驱动程序将自动启用 SSL 加密时运行上正确配置 Java 虚拟机 (JVM)，或其他的连接被终止和驱动程序将引发错误。  
  
> [!NOTE]  
>  请确保传递给值**serverName**完全匹配的公用名 (CN) 或 DNS 名称中使用者备用名称 (SAN) SSL 连接的服务器证书中才能成功。  
  
> [!NOTE]  
>  有关如何配置 SSL 的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅加密对连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="remarks"></a>注释  
 若要允许应用程序使用 SSL 加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]引入了以下连接属性从版本 1.2 发行版开始：**加密**， **trustServerCertificate**， **trustStore**， **trustStorePassword**，和**hostNameInCertificate**。 有关详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 下表总结了如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]版本的行为的可能的 SSL 连接方案。 每种方案使用一组不同的 SSL 连接属性。 该表包含：  
  
-   **空白**:"属性中不存在的连接字符串"  
  
-   **值**:"的连接字符串中存在的属性，其值为有效"  
  
-   **任何**:"并不重要是否连接字符串中存在的属性或其值无效"  
  
> [!NOTE]  
>  相同的行为适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用户身份验证和 Windows 集成身份验证。  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|行为|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false 或 blank|any|any|any|any|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不会强制[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]若要支持 SSL 加密。 如果服务器具有自签名证书，驱动程序将启动 SSL 证书交换。 将不会验证 SSL 证书，而只加密登录数据包中的凭据。<br /><br /> 如果服务器要求客户端支持 SSL 加密，驱动程序将启动 SSL 证书交换。 将不验证 SSL 证书，但将加密整个通信。|  
|true|true|any|any|any|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。 请注意，如果**trustServerCertificate**属性设置为"true"，该驱动程序将不验证 SSL 证书。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|blank|blank|blank|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**serverName**要验证服务器 SSL 证书，并依赖于的信任管理器工厂查找规则，以确定要使用的证书存储区的连接 URL 上指定的属性。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|值|blank|blank|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 该驱动程序将使用指定的值验证 SSL 证书的使用者值**hostNameInCertificate**属性。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|blank|值|值|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStore**要查找证书信任库文件的属性值和**trustStorePassword**属性值来检查信任库文件的完整性。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|blank|blank|值|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStorePassword**属性值，以检查默认信任库文件的完整性。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|blank|值|blank|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStore**属性值来查找 trustStore 文件的位置。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|值|blank|值|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStorePassword**属性值，以检查默认信任库文件的完整性。 此外，使用该驱动程序将**hostNameInCertificate**要验证的 SSL 证书的属性值。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|值|值|blank|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStore**属性值来查找 trustStore 文件的位置。 此外，使用该驱动程序将**hostNameInCertificate**要验证的 SSL 证书的属性值。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
|true|false 或 blank|值|值|值|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]请求以使用 SSL 加密与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果服务器要求客户端支持 SSL 加密，或者服务器支持加密，则驱动程序将启动 SSL 证书交换。<br /><br /> 驱动程序将使用**trustStore**要查找证书信任库文件的属性值和**trustStorePassword**属性值来检查信任库文件的完整性。 此外，使用该驱动程序将**hostNameInCertificate**要验证的 SSL 证书的属性值。<br /><br /> 如果服务器未配置为支持加密，驱动程序将报错并终止连接。|  
  
 如果加密属性设置为**true**、 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JVM 的默认 JSSE 安全提供程序用于协商使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 默认的安全提供程序可能不支持成功协商 SSL 加密所需的全部功能。 例如，默认安全提供程序可能不支持使用中的 RSA 公钥的大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。 在这种情况下，默认的安全提供程序可能报错，此错误将导致 JDBC 驱动程序终止连接。 为了解决这一问题，请执行下列操作之一：  
  
-   配置[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的较小的 RSA 公钥的服务器证书  
  
-   配置用于中的不同 JSSE 安全提供程序的 JVM"\<java 主页 > / lib/security/java.security"安全属性文件  
  
-   使用其他 JVM  
  
## <a name="validating-server-ssl-certificate"></a>验证服务器 SSL 证书  
 SSL 握手期间服务器向客户端发送其公钥证书。 JDBC 驱动程序或客户端必须验证服务器证书是由客户端信任的证书颁发机构颁发的。 驱动程序要求服务器证书必须满足以下条件：  
  
-   证书是由受信任的证书颁发机构颁发的。  
  
-   必须颁发证书才能进行服务器身份验证。  
  
-   证书未过期。  
  
-   公用名 (CN) 主题中或 DNS 名称中使用者备用名称 (SAN) 证书的完全匹配**serverName**连接字符串中指定的值，如果指定，则**hostNameInCertificate**属性值。  
  
-   DNS 名称可包含通配符。 但[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不支持通配符匹配。 也就是说，abc.com 将不匹配 *.com 但\*.com 将匹配\*。 com。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)   
 [保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
