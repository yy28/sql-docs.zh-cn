---
description: supportsUnion 方法 (SQLServerDatabaseMetaData)
title: supportsUnion 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsUnion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a757ea51-ff2e-4848-adaf-d9373e418fa3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99c8057d86d124cb2629c7463a85cb6e304437fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353973"
---
# <a name="supportsunion-method-sqlserverdatabasemetadata"></a>supportsUnion 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持 SQL UNION。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsUnion()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsUnion 方法是由 java.sql.DatabaseMetaData 接口中的 supportsUnion 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
