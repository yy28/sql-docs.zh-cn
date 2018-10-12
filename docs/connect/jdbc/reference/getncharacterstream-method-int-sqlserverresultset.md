---
title: getNCharacterStream 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1cfa4e4-3e1f-4504-b0de-cc626d653661
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 346039437c56c249bb4d030df5f9235aaf666331
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732536"
---
# <a name="getncharacterstream-method-int-sqlserverresultset"></a>getNCharacterStream 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列作为 Reader 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getNCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个读取器对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getNCharacterStream 方法由 java.sql.ResultSet 接口中的 getNCharacterStream 方法指定。  
  
 此方法可以用于检索的值**nvarchar**， **nchar**， **nvarchar （max)**， **ntext**，或**xml**的当前行中的列[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 如果尝试使用此方法检索其他数据类型的值，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
