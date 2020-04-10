---
title: getSchemaName 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getSchemaName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2d0063ab-d5d7-420f-b388-36d5169b1358
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 407f993aba800e3835eb92fe6b9539818a26d2fe
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921750"
---
# <a name="getschemaname-method-sqlserverresultsetmetadata"></a>getSchemaName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取指定列的表架构名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSchemaName(int column)  
```  
  
#### <a name="parameters"></a>parameters  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个包含架构名称的字符串  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getSchemaName 方法由 java.sql.ResultSetMetaData 接口中的 getSchemaName 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
