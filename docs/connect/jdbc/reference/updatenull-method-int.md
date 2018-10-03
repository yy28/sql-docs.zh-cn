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
manager: craigg
ms.openlocfilehash: 976edcbc2ca1a63bbe58d9d8d42a543d843a57b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690407"
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
  
 指示列索引的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateNull 方法由 java.sql.ResultSet 接口中的 updateNull 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateNull 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
