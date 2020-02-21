---
title: 设置为日期值的 setDate 方法 - int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setDate (int, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 12e5a4cc-45a2-4779-bbfc-e4da66829588
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 276533dcda2cf4524ee23f07ac2f102a56c3b788
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974718"
---
# <a name="setdate-method-int-javasqldate"></a>setDate 方法 (int, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的日期值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setDate(int n,  
                          java.sql.Date x)  
```  
  
#### <a name="parameters"></a>parameters  
 *n*  
  
 指示参数编号的 int  。  
  
 *x*  
  
 Date 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setDate 方法是由 java.sql.PreparedStatement 接口中的 setDate 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setDate 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
