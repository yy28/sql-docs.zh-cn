---
title: getUnicodeStream 方法 (SQLServerResultSet) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 406c3eea46a84f4931560e9187b146bb4718ded7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839342"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>getUnicodeStream 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中指定的列的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)为 Unicode 字符流的对象。  
  
> [!NOTE]  
>  此方法在 JDBC 规范中已不推荐使用，调用它将导致引发“尚未实现”异常。 相反，应使用[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)方法。  
  
## <a name="overload-list"></a>重载列表  
  
|名称|Description|  
|----------|-----------------|  
|[getUnicodeStream 方法&#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)为 Unicode 字符流的对象。|  
|[getUnicodeStream 方法&#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)为 Unicode 字符流的对象。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
