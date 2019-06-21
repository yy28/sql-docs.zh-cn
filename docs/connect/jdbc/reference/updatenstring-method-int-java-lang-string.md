---
title: updateNString 方法 （int，java.lang.String） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1bb909f1-4a96-4be1-adea-36c8d9703112
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c00621a2fedce7d9fba4d65f248b412627ee6233
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776657"
---
# <a name="updatenstring-method-int-javalangstring"></a>updateNString 方法 (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据指定的列索引，使用 String  值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNString(int columnIndex,  
                        java.lang.String nString)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 nString   
  
 一个**字符串**对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateNString 方法由 java.sql.ResultSet 接口中的 updateNString 方法指定。  
  
 此方法将传递 Java**字符串**到所选**nchar**， **nvarchar （max)** ， **ntext**，并**xml**列。 在其他数据类型列上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [updateNString 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
