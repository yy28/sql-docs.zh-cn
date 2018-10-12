---
title: getFetchSize 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc43780fc7864614c550a0192f363219823376c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776255"
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索结果集行数，该行数是由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成的结果集对象的默认提取大小。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>返回值  
 指示提取大小的 int，该提取大小由 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) 方法指定。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getFetchSize 方法由 java.sql.Statement 接口中的 getFetchSize 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
