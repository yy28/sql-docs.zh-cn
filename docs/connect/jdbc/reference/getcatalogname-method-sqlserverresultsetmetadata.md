---
title: getCatalogName 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getCatalogName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 64f62569-5d8e-411f-a98d-ddc52798391e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcf7c0b513726db49615b8ab85e99493b8a7cb41
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730485"
---
# <a name="getcatalogname-method-sqlserverresultsetmetadata"></a>getCatalogName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取包括指定列的表的目录名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getCatalogName(int column)  
```  
  
#### <a name="parameters"></a>Parameters  
 *column*  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个包含目录名称的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getCatalogName 方法由 java.sql.ResultSetMetaData 接口中的 getCatalogName 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
