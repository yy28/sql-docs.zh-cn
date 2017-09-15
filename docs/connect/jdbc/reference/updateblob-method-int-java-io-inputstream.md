---
title: "updateBlob 方法 （int、 java.io.InputStream） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0263018-d326-4a7b-bf6f-5f508db899d4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd8fe5107041959e95493adcab96175058c25523
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updateblob-method-int-javaioinputstream"></a>updateBlob 方法 (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定输入流更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBlob(int columnIndex,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
 *inputStream*  
  
 一个 InputStream 对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateBlob 方法指定此 updateBlob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateBlob 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
