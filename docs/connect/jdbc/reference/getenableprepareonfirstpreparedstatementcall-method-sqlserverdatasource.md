---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource) |Microsoft 文档
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
ms.openlocfilehash: a131964479c0e2f64afa1f316344d446d1df2214
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834538"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的值**enablePrepareOnFirstPreparedStatementCall**连接属性。 如果此配置，则返回 false 已准备的语句在首次执行将调用 sp_executesql 并做好准备一条语句，一旦第二次执行发生在它将调用 sp_prepexec 和实际安装程序已准备的语句句柄。 以下执行将调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。 
  
## <a name="syntax"></a>语法  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>返回值  
 返回**布尔**值**enablePrepareOnFirstPreparedStatementCall**连接属性。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>注释  
 此方法是从 JDBC 驱动程序版本 6.4 可用且开始。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
