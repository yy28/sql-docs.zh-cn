---
title: updateClob 方法 （int，java.io.Reader，long） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5c958ccb-386a-4dd5-901d-5a106dac2683
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42ea206399243d9844245b885f0a5c5fda95cbed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724617"
---
# <a name="updateclob-method-int-javaioreader-long"></a>updateClob 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的具有指定数量字符的 Reader 对象更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateClob(int columnIndex,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
 reader  
  
 一个读取器对象。  
  
 *length*  
  
 参数数据中的字符数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateClob 方法由 java.sql.ResultSet 接口中的 updateClob 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
