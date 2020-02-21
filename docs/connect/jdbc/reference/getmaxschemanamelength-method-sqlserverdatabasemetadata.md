---
title: getMaxSchemaNameLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxSchemaNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fece19e9-3bf8-4299-9188-ac3df5ce9c19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edfc9491f7652674293ef0a54a058e601608aff5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982029"
---
# <a name="getmaxschemanamelength-method-sqlserverdatabasemetadata"></a>getMaxSchemaNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库在架构名称中允许的最大字符数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxSchemaNameLength()  
```  
  
## <a name="return-value"></a>返回值  
 指示允许的最大字符数的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getMaxSchemaNameLength 方法是由 java.sql.DatabaseMetaData 接口中的 getMaxSchemaNameLength 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
