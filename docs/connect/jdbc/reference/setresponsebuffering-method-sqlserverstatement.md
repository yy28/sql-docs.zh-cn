---
title: "setResponseBuffering 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation: SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a8a3eb698ac0de46e3ffe88b36222bc5d618659
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置此缓冲模式响应[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)到不区分大小写的对象**字符串完整**或**自适应**。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *值*  
  
 A**字符串**包含响应缓冲模式。 有效的模式可以是以下不区分大小写的字符串之一：**完整**或**自适应**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 **自适应**指定缓冲最小可能的数据在必要时。  
  
 **完整**指定在运行时从服务器读取整个结果。  
  
 自适应是 JDBC 驱动程序版本 2.0 和 3.0 中的默认值。 JDBC 驱动程序版本 2.0 之前默认值是完整。  
  
 [SetResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法允许你重写**responseBuffering**连接**字符串**属性当前[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
 如果应用程序将指定为无效的参数值[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法， [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)引发。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
