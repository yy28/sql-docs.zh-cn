---
title: setHostNameInCertificate 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: deeab57c573311db36eabdbad60c3cb2fbda9a47
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974222"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置要用于验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全套接字层 (SSL) 证书的主机名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>parameters  
 *hostNameInCertificate*  
  
 一个包含主机名的字符串  。  
  
## <a name="remarks"></a>备注  
 当使用 SSL 对通信层加密时，将使用 hostNameInCertificate 值来验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书。 默认值为 null。  
  
 如果 hostNameInCertificate 属性设置为 Null 或未指定，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将使用 serverName 属性值来对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书进行验证。 如果 hostNameInCertificate 属性被设置为字符串或空字符串 ("")，则驱动程序将使用该值验证服务器 SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
