---
title: getURL 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getURL (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d0b665c-e1a7-43f7-88c3-db432773de7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8dec0c47a9a5954d934dc8ba8a687af76cb319f2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910723"
---
# <a name="geturl-method-int-sqlserverresultset"></a>getURL 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 URL 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.net.URL getURL(int columnIndex)  
```  
  
#### <a name="parameters"></a>parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 URL 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getURL 方法是由 java.sql.ResultSet 接口中的 getURL 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getURL 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
