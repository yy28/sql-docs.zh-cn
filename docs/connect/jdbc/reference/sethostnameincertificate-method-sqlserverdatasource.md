---
title: "setHostNameInCertificate 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: setHostNameInCertificate Method (SQLServerDataSource)
apilocation: setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6809bd1bc1bde04e7080679b54bb2c316048ad4a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置要在验证中使用的主机名[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]安全套接字层 (SSL) 证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parameters  
 *hostNameInCertificate*  
  
 A**字符串**，其中包含的主机名。  
  
## <a name="remarks"></a>注释  
 HostNameInCertificate 值用于验证[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 证书时使用 SSL 进行加密的通信层。 默认值为 null。  
  
 如果 hostNameInCertificate 属性设置为 null 或未指定，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将使用的 serverName 属性值来验证对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 证书。 如果 hostNameInCertificate 属性被设置为字符串或空字符串 ("")，则驱动程序将使用该值验证服务器 SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
