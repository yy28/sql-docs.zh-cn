---
title: setLong 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08223a62-6489-44e4-85e8-b45bfbb11cfc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 347f0eb1d35c2a9662fa4384d6f6bab46bae5003
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925730"
---
# <a name="setlong-method-sqlserverpreparedstatement"></a>setLong 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 long  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setLong(int n,  
                          long x)  
```  
  
#### <a name="parameters"></a>parameters  
 *n*  
  
 指示参数编号的 int  。  
  
 *x*  
  
 long  值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setLong 方法是由 java.sql.PreparedStatement 接口中的 setLong 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
