---
title: getFetchDirection 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f56893764392236d563fa2b9a236f55e67e13595
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983252"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的提取方向。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>返回值  
 指示当前提取方向的 int  值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getFetchDirection 方法是由 java.sql.ResultSet 接口中的 getFetchDirection 方法指定的。  
  
 此方法对只进游标返回 FETCH_FORWARD，对于其他游标类型返回调用 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) 方法所指定的最后设置。如果从未调用 setFetchDirection 方法，则为这些游标类型返回 FETCH_UNKNOWN。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
