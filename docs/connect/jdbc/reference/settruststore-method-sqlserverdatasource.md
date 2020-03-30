---
title: setTrustStore 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be54aea70e712d2209c04196d3e450bca488578b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972191"
---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指向证书 trustStore 文件的路径（包括文件名）。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>parameters  
  trustStore  
  
 包含证书 trustStore 文件的路径（包括文件名）的字符串  。  
  
## <a name="remarks"></a>备注  
 如果未指定 trustStore 属性或将此属性设置为 null，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将依赖于信任关系管理器工厂的查找规则来确定要使用哪一个证书存储区。 默认的 SunX509 TrustManagerFactory 尝试按此顺序在下列位置查找信任的资料：  
  
-   1. 由“javax.net.ssl.trustStore”Java 虚拟机 (JVM) 系统属性指定的文件。  
  
-   2. “\<java-home>/lib/security/jssecacerts”文件。  
  
-   3. “\<java-home>/lib/security/cacerts”文件。  
  
 有关详细信息，请参阅 Sun Microsystems 网站上的 SunX509 TrustManager 接口文档。  
  
 如果将 trustStore 属性设置为字符串或空字符串 ""，则驱动程序将使用该值来查找 trustStore 文件以验证服务器 SSL 证书。  
  
 可随 trustStore 属性同时指定 trustStorePassword 属性，并使用其值来打开 trustStore 文件。 有关详细信息，请参阅 [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
