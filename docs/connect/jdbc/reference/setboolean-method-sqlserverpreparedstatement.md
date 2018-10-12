---
title: setBoolean 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBoolean
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 63397a19-03a2-44bb-b661-7d62c95b6e4e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5be9d4dfdb6760cba13556a1de38db12258c5cfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798855"
---
# <a name="setboolean-method-sqlserverpreparedstatement"></a>setBoolean 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setBoolean(int n,  
                             boolean x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *n*  
  
 指示参数编号的 int。  
  
 *x*  
  
 一个**布尔**值，要么**true**或**false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setboolean 方法是由 java.sql.PreparedStatement 接口中的 setboolean 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
