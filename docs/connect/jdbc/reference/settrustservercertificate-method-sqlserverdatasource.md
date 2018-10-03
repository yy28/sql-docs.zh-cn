---
title: setTrustServerCertificate 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 313e763fd82b1bf8515fcb5f7a850d84da260de9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793730"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置一个布尔值，此值指示是否启用了 trustServerCertificate 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parameters  
 *trustServerCertificate*  
  
 如果当使用安全套接字层 (SSL) 对通信层加密时应自动信任服务器安全套接字层证书，则为“true”。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果将 trustServerCertificate 属性设置为“true”，则当使用 SSL 对通信层加密时将自动信任 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书。 换言之，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将不会验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书。 默认值是 **false**秒。  
  
 如果将 trustServerCertificate 属性设置为“false”，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将验证服务器 SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
