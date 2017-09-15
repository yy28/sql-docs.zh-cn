---
title: "setTrustStore 方法 (SQLServerDataSource) |Microsoft 文档"
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
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e6de008468da81facf98c039457f9248ddddc49
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指向证书 trustStore 文件的路径（包括文件名）。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>Parameters  
 *信任库*  
  
 A**字符串**包含到证书信任库文件的路径 （包括文件名称）。  
  
## <a name="remarks"></a>注释  
 如果 trustStore 属性为未指定或未设置为 null，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将依赖于的信任管理器工厂查找规则以确定要使用的证书存储区。 默认值 SunX509 TrustManagerFactory 尝试查找信任材料，还在以下位置按以下顺序：  
  
-   1. 由“javax.net.ssl.trustStore”Java 虚拟机 (JVM) 系统属性指定的文件。  
  
-   2. "\<java 主页 >/lib/安全/jssecacerts"文件。  
  
-   3. "\<java 主页 >/lib/安全/cacerts"文件。  
  
 有关详细信息，请参阅 Sun Microsystems 网站上的 SunX509 TrustManager 接口文档。  
  
 如果将 trustStore 属性设置为字符串或空字符串 ""，则驱动程序将使用该值来查找 trustStore 文件以验证服务器 SSL 证书。  
  
 可随 trustStore 属性同时指定 trustStorePassword 属性，并使用其值来打开 trustStore 文件。 有关详细信息，请参阅[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
