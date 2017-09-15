---
title: "setTrustStorePassword 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d42539e3a0979500c28539d256226624ac6997eb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>setTrustStorePassword 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于检查 trustStore 数据完整性的密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>Parameters  
 *trustStorePassword*  
  
 A**字符串**包含用于检查 trustStore 数据的完整性的密码。  
  
## <a name="remarks"></a>注释  
 可随 trustStore 属性同时指定 trustStorePassword 属性，并使用其值来检查 trustStore 文件的完整性。  
  
 如果设置了 trustStore 属性，但未设置 trustStorePassword 属性，则不检查 trustStore 的完整性。  
  
 如果未指定 trustStore 和 trustStorePassword 属性，驱动程序将使用 Java 虚拟机 (JVM) 系统属性“javax.net.ssl.trustStore”和“javax.net.ssl.trustStorePassword”。 如果未指定“javax.net.ssl.trustStorePassword”系统属性，则不检查 trustStore 的完整性。  
  
 如果未指定 trustStore 属性，但设置了 trustStorePassword 属性，JDBC 驱动程序将使用由“javax.net.ssl.trustStore”指定作为信任存储区的文件，并使用指定的 trustStorePassword 检查信任存储区的完整性。 当客户端应用程序不希望在 JVM 系统属性中存储密码时，这一点可能是必需的。  
  
 有关详细信息，请参阅[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 从 JDBC Driver 3.0 开始，如果您在绑定数据源属性前设置 SQLServerDataSource.setTrustStorePassword，在获取连接前必须调用 SQLServerDataSource.setTrustStorePassword。 有关详细信息，请参阅[SQLServerDataSource.getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
