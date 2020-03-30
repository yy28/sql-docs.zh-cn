---
title: relative 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b2e644feff3cd2787cc6bd80bce54562ad20794
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975780"
---
# <a name="relative-method-sqlserverresultset"></a>relative 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将游标沿正向或反向移动相对于当前行的指定行数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>parameters  
 nRows   
  
 指示要移动的行数的 int  。  
  
## <a name="return-value"></a>返回值  
 如果游标在行上，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 relative 方法是由 java.sql.ResultSet 接口中的 relative 方法指定的。  
  
 如果尝试移到结果集中的第一行之前或最后一行之后，将使游标移到第一行之前或最后一行之后。 调用 `relative(0)` 有效，但是不会更改游标位置。  
  
 调用 `relative(1)` 方法与调用 [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) 方法效果相同。 调用 `relative(-1)` 方法与调用 [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) 方法效果相同。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
