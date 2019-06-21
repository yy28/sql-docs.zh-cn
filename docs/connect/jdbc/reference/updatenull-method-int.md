---
title: updateNull 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateNull (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b22336a1-fe53-4e00-a5ff-ede8d3f2b9f9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3e1b4b391cf0c2106a705e272d891158c8ab5e3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798815"
---
# <a name="updatenull-method-int"></a>updateNull 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列索引使用 Null 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNull(int index)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示列索引的 int  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateNull 方法是由 java.sql.ResultSet 接口中的 updateNull 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateNull 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
