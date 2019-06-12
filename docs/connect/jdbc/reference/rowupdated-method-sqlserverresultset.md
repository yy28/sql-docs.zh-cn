---
title: getBigDecimal 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b827ebb9740c9d88017c5d47626b9a1cef493143
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765264"
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索当前行是否已更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>返回值  
 如果行已由所有者或其他用户可见地更新了并且更新被检测到了，则为**true**。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 rowUpdated 方法由 java.sql.ResultSet 接口中的 rowUpdated 方法指定。  
  
 返回的值取决于结果集是否可以检测更新。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不检测任何游标类型的已更新行。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
