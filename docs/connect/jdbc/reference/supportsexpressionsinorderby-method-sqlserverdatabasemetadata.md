---
title: supportsExpressionsInOrderBy 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsExpressionsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 858f3c02-4531-4775-97e9-a03b316bdaba
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01c9bfaadfee95369fb0101140c03d35fc777420
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969430"
---
# <a name="supportsexpressionsinorderby-method-sqlserverdatabasemetadata"></a>supportsExpressionsInOrderBy 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持 ORDER BY 列表中的表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsExpressionsInOrderBy()  
```  
  
## <a name="return-value"></a>返回值  
 如果支持，则值为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 supportsExpressionsInOrderBy 方法是由 java.sql.DatabaseMetaData 接口中的 supportsExpressionsInOrderBy 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
