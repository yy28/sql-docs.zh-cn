---
title: updateNCharacterStream 方法 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 504d7d06-0227-45e1-8b01-899c3e6006e8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7139fbe6caff5e8f30bb93aa6739db0f713a120
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798438"
---
# <a name="updatencharacterstream-method-javalangstring-javaioreader"></a>updateNCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnLabel   
  
 一个包含列标签的字符串  。  
  
 reader   
  
 Reader 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateNCharacterStream 方法由 java.sql.ResultSet 接口中的 updateNCharacterStream 方法指定。  
  
 此方法将来自要选择的读取器对象中传递 Unicode 字符**nchar**， **nvarchar （max)** ， **ntext**并**xml**列。 在其他数据类型列上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [updateNCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
