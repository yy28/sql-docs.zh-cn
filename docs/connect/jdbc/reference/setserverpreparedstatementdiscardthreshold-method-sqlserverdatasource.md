---
title: setServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96c5454ed116c8e7264f475b6488db29bab66a9c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927798"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>setServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置 serverPreparedStatementDiscardThreshold 连接属性的值。 此设置控制在执行调用以清除服务器上未完成的句柄之前，每个连接可以有多少个未完成的预定义语句放弃操作 (sp_unprepare) 处于未处理状态。 如果设置 <= 1，则在预定义语句关闭时将立即执行 unprepare 操作。 如果将该值设置为 > 1，则这些调用将一起进行批处理，以避免过于频繁地调用 sp_unprepare 的开销
 
## <a name="syntax"></a>语法  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>parameters  
 *serverPreparedStatementDiscardThreshold*  
  
 serverPreparedStatementDiscardThreshold  连接属性的新值。  

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>备注  
 JDBC 驱动程序版本 6.4 及其后续版本中提供此方法。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
