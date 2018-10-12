---
title: getResponseBuffering 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c682e28244bf85ce761ab6f8d0b54d5f5f054679
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680405"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的响应缓冲模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>返回值  
 一个 String，其中包含小写“full”或“adaptive”。  
  
## <a name="remarks"></a>Remarks  
 “adaptive”指定在必要时缓冲尽可能少的数据。  
  
 “full”指定在运行时从服务器读取全部结果。  
  
 **adaptive** 是 JDBC Driver 2.0 和 3.0 版本中的默认值。 **full** 是 JDBC Driver 2.0 版之前。  
  
 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setResponseBuffering 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
