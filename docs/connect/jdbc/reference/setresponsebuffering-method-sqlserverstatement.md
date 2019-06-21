---
title: setResponseBuffering 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5b4490ac15558a0f6268a3d400d197367d028b9d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796746"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的响应缓冲模式设置为不区分大小写的“String full”  或“adaptive”  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *value*  
  
 包含响应缓冲模式的 String  。 有效模式可以为下列不区分大小写的字符串之一：“full”  或“adaptive”  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 “adaptive”  指定在必要时缓冲尽可能少的数据。  
  
 “full”  指定在运行时从服务器读取全部结果。  
  
 adaptive 是 JDBC 驱动程序版本 2.0 和 3.0 中的默认值。 full 是版本低于 2.0 的 JDBC 驱动程序中的默认值。  
  
 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法允许覆盖当前 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 responseBuffering  连接 String  属性。 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
 如果应用程序为 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法指定无效的参数值，则会引发 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
