---
description: isCatalogAtStart 方法 (SQLServerDatabaseMetaData)
title: isCatalogAtStart 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.isCatalogAtStart
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 665173d2-14c7-4ce1-954e-4adb53fb9b39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 115131b5d99d331ca4d0137978d471b2723efc1e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433609"
---
# <a name="iscatalogatstart-method-sqlserverdatabasemetadata"></a>isCatalogAtStart 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索目录是否出现在完全限定表名的开始位置。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isCatalogAtStart()  
```  
  
## <a name="return-value"></a>返回值  
 如果目录名称出现在开始位置，则为 true****。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isCatalogAtStart 方法是由 java.sql.DatabaseMetaData 接口中的 isCatalogAtStart 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
