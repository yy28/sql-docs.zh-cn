---
title: setEncrypt 方法 (SQLServerDataSource) |Microsoft 文档
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
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2462fc7c0e277a2cd22a168259068cb1ed74f889
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集**布尔**值，该值指示是否启用了加密属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parameters  
 *加密*  
  
 **true**如果客户端之间启用安全套接字层 (SSL) 加密与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果加密属性设置为**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]确保[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]如果服务器已安装的证书客户端和服务器之间发送的所有数据使用 SSL 加密。 默认值是 **false**秒。  
  
 JDBC 驱动程序在尝试建立 SSL 握手时，会检测运行它的 Java 虚拟机 (JVM)。  
  
 如果加密属性设置为**true**、 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] JVM 的默认 JSSE 安全提供程序用于协商使用 SSL 加密[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 默认的安全提供程序可能不支持成功协商 SSL 加密所需的全部功能。 例如，默认安全提供程序可能不支持使用中的 RSA 公钥的大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 证书。 在这种情况下，默认的安全提供程序可能报错，此错误将导致 JDBC 驱动程序终止连接。 为了解决这一问题，请执行下列操作之一：  
  
-   配置[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]的较小的 RSA 公钥的服务器证书  
  
-   配置用于中的不同 JSSE 安全提供程序的 JVM"\<java 主页 > / lib/security/java.security"安全属性文件  
  
-   使用其他 JVM  
  
 如果未指定或设置为加密属性**false**，驱动程序将不会强制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]若要支持 SSL 加密。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例未配置为强制 SSL 加密，而无需任何加密建立的连接。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例配置为强制 SSL 加密，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将自动启用 SSL 加密，在正常运行配置 JVM，否则的连接被终止时，编译器驱动程序将引发错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
