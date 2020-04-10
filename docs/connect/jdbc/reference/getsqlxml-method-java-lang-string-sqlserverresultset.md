---
title: getSQLXML 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9c7b10-026f-4a51-8d60-e6871d1abd02
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63872c5dcdf882797317755d407a70f9d250bdc7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80912043"
---
# <a name="getsqlxml-method-javalangstring-sqlserverresultset"></a>getSQLXML 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列作为 SQLXML 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>parameters  
 *columnName*  
  
 指示列标签的字符串  。  
  
## <a name="return-value"></a>返回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getSQLXML 方法是由 java.sql.ResultSet 接口中的 getSQLXML 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getSQLXML 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
