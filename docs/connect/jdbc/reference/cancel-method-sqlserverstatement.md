---
description: cancel 方法 (SQLServerStatement)
title: cancel 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44f59ea02a54f68833eb40b291d4cd8edeb56da6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438189"
---
# <a name="cancel-method-sqlserverstatement"></a>cancel 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取消当前正由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象运行的 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 cancel 方法由 java.sql.Statement 接口中的 cancel 方法指定。  
  
 当执行可生成单个大型只进、只读结果集的语句时，您所感兴趣的可能只是返回的结果集中的一些初始行集。 在此情况下，应用程序可能会在关闭结果集之前调用关联语句对象的 [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 方法，以最大程度地减少放弃余下不必要的行所需要的处理时间。 在决定是否应使用此方法时，建议对照可节约的处理时间与取消执行所需的时间及与服务器之间的附加往返，在两者之间进行折衷。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
