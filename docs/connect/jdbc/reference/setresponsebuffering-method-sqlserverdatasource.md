---
title: setResponseBuffering 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa4e1c6921495448ce0a1e01a972b1786a69efd9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796758"
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>setResponseBuffering 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置通过使用此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象创建的连接的响应缓冲模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *value*  
  
 包含缓冲和流模式的 String  。 有效模式可以为下列不区分大小写的字符串之一：“full”  或“adaptive”  。  
  
## <a name="remarks"></a>Remarks  
 指定在运行时从服务器读取全部结果的 full  值。  
  
 adaptive  值指定在必要时缓冲尽可能少的数据。 adaptive  值为默认缓冲模式。  
  
 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
