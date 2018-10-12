---
title: position 方法 (java.lang.String, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 46d4beec-831a-449f-98b6-322a80cc499a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b74fa32c08115ea67cd75a33db6f917ad0bb1bd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672563"
---
# <a name="position-method-javalangstring-long-sqlservernclob"></a>position 方法 (java.lang.String, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索的字符位置指定的子字符串*searchstr*将出现在**NCLOB**值由此**NClob**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public long position(java.lang.String searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parameters  
 *searchstr*  
  
 要搜索子字符串。  
  
 start  
  
 开始搜索的位置；第一个位置为 1。  
  
## <a name="return-value"></a>返回值  
 子字符串出现的位置，如果未出现，则为 -1。 第一个位置为 1。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此位置方法由 java.sql.NClob 接口中的位置方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [position 方法&#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
