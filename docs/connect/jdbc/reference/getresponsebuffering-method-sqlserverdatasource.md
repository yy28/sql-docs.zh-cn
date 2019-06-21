---
title: getResponseBuffering 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ea9552ff9a9bf8d0a591f35670ca7147c67e18d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801356"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回此 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象的响应缓冲模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>返回值  
 包含小写 full  或 adaptive  的 String  。  
  
## <a name="remarks"></a>Remarks  
 指定在运行时从服务器读取全部结果的 full  值。  
  
 adaptive  值指定在必要时缓冲尽可能少的数据。 adaptive  值为默认缓冲模式。  
  
 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setResponseBuffering 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
