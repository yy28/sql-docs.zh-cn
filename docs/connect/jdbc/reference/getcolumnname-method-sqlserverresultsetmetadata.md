---
description: getColumnName 方法 (SQLServerResultSetMetaData)
title: getColumnName 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0330ca1d-5e24-4ce3-9d2a-b931f20a0fcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9e3701e5905c2223cd77a9c9bcd30c2ca72042a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436559"
---
# <a name="getcolumnname-method-sqlserverresultsetmetadata"></a>getColumnName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取指定列的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getColumnName(int column)  
```  
  
#### <a name="parameters"></a>参数  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个包含列名的字符串  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getColumnName 方法是由 java.sql.ResultSetMetaData 接口中的 getColumnName 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
