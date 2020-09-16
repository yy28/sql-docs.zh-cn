---
description: nullsAreSortedLow 方法 (SQLServerDatabaseMetaData)
title: nullsAreSortedLow 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedLow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30c06a9d-3513-42d0-8b2a-5a20ac31eb0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33239e2f4755adb526b9b81158efd2498702452f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433129"
---
# <a name="nullsaresortedlow-method-sqlserverdatabasemetadata"></a>nullsAreSortedLow 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 NULL 值是否在排序中位置较低。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean nullsAreSortedLow()  
```  
  
## <a name="return-value"></a>返回值  
 如果该值在排序中位置较低，则为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 nullsAreSortedLow 方法是由 java.sql.DatabaseMetaData 接口中的 nullsAreSortedLow 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
