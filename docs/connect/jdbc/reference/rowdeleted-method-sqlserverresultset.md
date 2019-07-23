---
title: rowDeleted 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37221f0f9c7cf87576f0014b855ed28740e4818e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975714"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索是否已删除某行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>返回值  
 如果删除了某行并且检测到了删除，则为“true”  。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 rowDeleted 方法由 rowDeleted 方法在方法中指定。  
  
 已删除的行可能在结果集中留有可见孔。 此方法可用于检测结果集中的孔。 返回的值取决于此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象能否可以检测到删除。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将针对所有可更新的游标类型检测已删除的行，尽管此检测对于前进和动态游标是暂时的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
