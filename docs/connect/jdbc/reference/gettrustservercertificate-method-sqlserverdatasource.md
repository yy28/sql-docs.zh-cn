---
title: getTrustServerCertificate 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81d07743dfefe0b0305b1a094a9ae4632d4effd9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978578"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回一个布尔值，此值指示是否启用了 trustServerCertificate 属性  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>返回值  
 如果已启用 trustServerCertificate，则为“true”  。 否则为 **false**。  
  
## <a name="remarks"></a>备注  
 如果将 trustServerCertificate 属性设置为“true”，则当使用 SSL 对通信层加密时将自动信任 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全套接字层 (SSL) 证书  。 换言之，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将不会验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 证书。 默认值是 **false**秒。  
  
 如果将 trustServerCertificate 属性设置为“false”，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将验证服务器 SSL 证书  。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
