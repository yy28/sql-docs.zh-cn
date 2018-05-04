---
title: getTrustServerCertificate 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0d22963fc8e916bb554ba5bb385efe1abfcd84c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**布尔**值，该值指示是否启用了 trustServerCertificate 属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果启用 trustServerCertificate。 否则为 **false**。  
  
## <a name="remarks"></a>注释  
 如果 trustServerCertificate 属性设置为**true**、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]安全套接字层 (SSL) 证书是自动受信任的当使用 SSL 加密的通信层。 换而言之，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将不会验证[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 证书。 默认值是 **false**秒。  
  
 如果 trustServerCertificate 属性设置为**false**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]将验证服务器 SSL 证书。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
