---
title: getDisableStatementPooling 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6749c877718b32af88a1433342f044a8cd24f05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>getDisableStatementPooling 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的值**disableStatementPooling**连接属性。 此设置可控制是否启用语句池或不适用于此连接。

  
## <a name="syntax"></a>语法  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>返回值  
 A**布尔**包含值的**disableStatementPooling**连接属性。
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>注释  
 此方法是从 JDBC 驱动程序版本 6.4 可用且开始。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
