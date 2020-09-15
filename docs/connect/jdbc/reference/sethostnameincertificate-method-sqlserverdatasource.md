---
description: setHostNameInCertificate 方法 (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886a32898b04cc8907a832d54a3051222e4d0fb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431819"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 传输层安全性 (TLS)（以前称为安全套接字层 (SSL)）证书的主机名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>参数  
 *hostNameInCertificate*  
  
 一个包含主机名的字符串  。  
  
## <a name="remarks"></a>备注  
 使用 TLS 加密通信层时，hostNameInCertificate 值用于验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 证书。 默认值为 null。  
  
 如果 hostNameInCertificate 属性设置为 null 或未指定，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将使用 serverName 属性值针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 证书进行验证。 如果 hostNameInCertificate 属性设置为字符串或空字符串 ""，驱动程序将使用该值来验证服务器 TLS/SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
