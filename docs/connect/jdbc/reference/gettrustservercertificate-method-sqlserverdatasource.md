---
description: getTrustServerCertificate 方法 (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a5de057e6a9363f4e3feeace35f2b5105d3cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434049"
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
 如果 trustServerCertificate 属性设置为 true，使用 TLS 加密通信层时，将自动信任 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 传输层安全性 (TLS)（以前称为安全套接字层 (SSL)）证书  。 换言之，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将不会验证 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 证书。 默认值是 **false**秒。  
  
 如果将 trustServerCertificate 属性设置为 false，则 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 将验证服务器 TLS/SSL 证书  。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
