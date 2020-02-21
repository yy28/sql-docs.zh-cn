---
title: supportsConvert 方法 (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsConvert (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 54741cfd-32ac-46c5-8b09-fd60fd8833d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae22b0f4149536977dd3ee7c9cc21758e7dcc980
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969600"
---
# <a name="supportsconvert-method-int-int"></a>supportsConvert 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库对于两个给定的 SQL 类型是否支持 CONVERT。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsConvert(int fromType,  
                               int toType)  
```  
  
#### <a name="parameters"></a>parameters  
 fromType   
  
 要从其转换的 JDBC 类型。  
  
 toType   
  
 要转换到的 JDBC 类型。  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsConvert 方法是由 java.sql.DatabaseMetaData 接口中的 supportsConvert 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [supportsConvert 方法 (SQLServerDatabaseMetaData)](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)   
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
