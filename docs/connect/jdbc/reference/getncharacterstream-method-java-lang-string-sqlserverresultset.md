---
title: getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52e2f0336c2c4bfbe6b14ce116c0888844afc000
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784720"
---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列的值作为 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 一个包含列标签的 String。  
  
## <a name="return-value"></a>返回值  
 一个 Reader 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getNCharacterStream 方法由 java.sql.ResultSet 接口中的 getNCharacterStream 方法指定。  
  
 此方法可以用于检索的值**nvarchar**， **nchar**， **nvarchar （max)** ， **ntext**，或**xml**的当前行中的列[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 如果尝试使用此方法检索其他数据类型的值，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
