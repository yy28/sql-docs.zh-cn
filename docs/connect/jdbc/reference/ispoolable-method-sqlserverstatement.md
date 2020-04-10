---
title: isPoolable 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f0b0e45e24d1eb8ddf23b3b544d7f6e7b52d728
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925820"
---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回指示是否可以将语句添加到用户提供的语句池的一个值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>返回值  
 如果可以将该语句添加到用户提供的语句池，则为 true  ；否则为 false  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) 将更改对象的可入池行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
