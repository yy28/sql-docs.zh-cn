---
title: setEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26ac2cac075d08b8029ac0e85dacffd1674fb0da
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974313"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>setEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定特定连接实例的行为。 如果此配置为 false，则第一次执行预定义语句时，将调用 sp_executesql 而不是预定义语句，发生第二次执行后，它随即调用 sp_prepexec 并实际设置一个预定义语句句柄。 以下执行将调用 sp_execute。 如果该语句仅执行一次，则无需在预定义语句关闭时使用 sp_unprepare。  
## <a name="syntax"></a>语法  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>parameters  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 enablePrepareOnFirstPreparedStatementCall  连接属性的新值。  

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>备注  
 JDBC 驱动程序版本 6.4 及其后续版本中提供此方法。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
