---
description: getUnicodeStream 方法 (SQLServerResultSet)
title: getUnicodeStream 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43590c9d660a54d24c42b8032ee886ffcd587ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433909"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>getUnicodeStream 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列的值作为 Unicode 字符流。  
  
> [!NOTE]  
>  此方法在 JDBC 规范中已不推荐使用，调用它将导致引发“尚未实现”异常。 应改用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法。  
  
## <a name="overload-list"></a>重载列表  
  
|名称|说明|  
|----------|-----------------|  
|[getUnicodeStream 方法 &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Unicode 字符流的值。|  
|[getUnicodeStream 方法 &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 Unicode 字符流的值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
