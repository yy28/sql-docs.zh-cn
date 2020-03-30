---
title: getResponseBuffering 方法 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 4b3e53579b8c95cce0585e9614152053f39cafa8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980432"
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
  
## <a name="remarks"></a>备注  
 指定在运行时从服务器读取全部结果的 full  值。  
  
 adaptive  值指定在必要时缓冲尽可能少的数据。 adaptive  值为默认缓冲模式。  
  
 有关使用响应缓冲模式的详细信息，请参阅[使用自适应缓冲](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setResponseBuffering 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
