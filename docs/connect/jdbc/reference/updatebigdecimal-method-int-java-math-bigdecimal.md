---
title: updateBigDecimal 方法 (int, java.math.BigDecimal) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBigDecimal (int, java.math.BigDecimal)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e15de27-a490-45cd-a3a6-a49721f15a97
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 45aca6d7ff7806ed2315e4b582ce4f724927bb1b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798876"
---
# <a name="updatebigdecimal-method-int-javamathbigdecimal"></a>updateBigDecimal 方法 (int, java.math.BigDecimal)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列索引使用 BigDecimal 对象更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBigDecimal(int index,  
                             java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示列索引的 int  。  
  
 *x*  
  
 一个 BigDecimal 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBigDecimal 方法由 java.sql.ResultSet 接口中的 updateBigDecimal 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateBigDecimal 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
