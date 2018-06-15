---
title: supportsMultipleOpenResults 方法 (SQLServerDatabaseMetaData) |Microsoft 文档
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
- SQLServerDatabaseMetaData.supportsMultipleOpenResults
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9480d280-5e3d-46ae-80e6-1bba3ac5a641
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c928e50a5035ed6e192e08b5b83a877f3d41c92d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32847552"
---
# <a name="supportsmultipleopenresults-method-sqlserverdatabasemetadata"></a>supportsMultipleOpenResults 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可能存在多个是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)从返回的对象[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)同时对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsMultipleOpenResults()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 supportsMultipleOpenResults 方法指定此 supportsMultipleOpenResults 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
