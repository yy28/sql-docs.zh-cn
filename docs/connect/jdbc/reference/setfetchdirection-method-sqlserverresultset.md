---
title: setFetchDirection 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d801a0184259ae22f86ea5ec23391ef78b23ce38
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974266"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供提示以指明将用于处理此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的行的方向。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支持此方法。 如果使用此方法，则 JDBC 驱动程序将记住该设置，但目前不进行处理。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>parameters  
 direction   
  
 指示建议的提取方向的 int  。 可以是以下值之一：  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setFetchDirection 方法是由 java.sql.ResultSet 接口中的 setFetchDirection 方法指定的。  
  
 此方法的初始值是由生成此 SQLServerResultSet 对象的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象确定的。 可以随时更改提取方向。  
  
> [!NOTE]  
>  当游标类型为只进时，使用此方法将不起作用。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
