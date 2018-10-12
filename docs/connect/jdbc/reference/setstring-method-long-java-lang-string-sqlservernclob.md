---
title: setString 方法 (long，java.lang.String)-NClob |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 151ff8f36ad3397321dc168b46a949de38e10bd6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689895"
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>setString 方法 (long, java.lang.String) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  写入指定**字符串**到**NCLOB**从指定位置开始。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>Parameters  
 *pos*  
  
 写入 NCLOB 的起始位置；第一个位置为 1。  
  
 *str*  
  
 要写入 NCLOB 的 String。  
  
## <a name="return-value"></a>返回值  
 写入的字符数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setString 方法由 java.sql.NClob 接口中的 setString 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
