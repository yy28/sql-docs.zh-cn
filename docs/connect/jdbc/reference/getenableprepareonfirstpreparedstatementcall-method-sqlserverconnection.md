---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 203ed2f6a68e11af8c63157a850a146ea8d81464
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909579"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 返回 enablePrepareOnFirstPreparedStatementCall  连接属性的值。 如果为 false，则第一次执行将调用 sp_executesql 而不准备语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个准备好的语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 来更改此选项的默认值。

## <a name="syntax"></a>语法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>返回值
 一个布尔值  ，其中包含 enablePrepareOnFirstPreparedStatementCall  连接属性的值。

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>备注  
 JDBC 驱动程序版本 6.4 及其后续版本中提供此方法。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
