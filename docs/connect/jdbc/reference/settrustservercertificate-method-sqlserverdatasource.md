---
title: setTrustServerCertificate 方法 (SQLServerDataSource) |Microsoft 文档
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
ms.topic: article
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b4a1788fc4e4578cf8b80893d6d1f2c80fa6e3e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集**布尔**值，该值指示是否启用了 trustServerCertificate 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parameters  
 *TrustServerCertificate*  
  
 **true**如果在使用 SSL 加密的通信层时，服务器安全套接字层 (SSL) 证书应为自动受信任。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 trustServerCertificate 属性设置为**true**、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 证书是自动受信任的当使用 SSL 加密的通信层。 换而言之，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将不会验证[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 证书。 默认值是 **false**秒。  
  
 如果 trustServerCertificate 属性设置为**false**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将验证服务器 SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
