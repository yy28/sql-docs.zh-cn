---
title: nullsAreSortedAtEnd 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedAtEnd
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 713cf636-40f2-474a-8a5d-5aba4a310a9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871f7896f0f0053e8b45bd93dedd5153a58b8b25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673275"
---
# <a name="nullsaresortedatend-method-sqlserverdatabasemetadata"></a>nullsAreSortedAtEnd 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索是否无论排序顺序如何 NULL 值始终排在最后。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean nullsAreSortedAtEnd()  
```  
  
## <a name="return-value"></a>返回值  
 如果排在最后，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 nullsAreSortedAtEnd 方法由 java.sql.DatabaseMetaData 接口中的 nullsAreSortedAtEnd 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
