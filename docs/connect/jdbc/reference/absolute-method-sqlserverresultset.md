---
title: absolute 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 298e169fe2b67b16b55d607f504446c48893fc1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616935"
---
# <a name="absolute-method-sqlserverresultset"></a>absolute 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将游标移到此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的给定行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>Parameters  
 row  
  
 指示要移到的行号的 int 值。 它可以为正数、负数或 0。  
  
## <a name="return-value"></a>返回值  
 **true**如果将光标移到给定位置。 **false**如果它是第一行之前或最后一行之后。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此绝对方法由 java.sql.ResultSet 接口中的绝对方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
