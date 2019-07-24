---
title: getNCharacterStream 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6ae704f5-823c-4dfe-8c08-07b547c61a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ed91df645edd7083e0d91346dfdf6d39bebd91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981649"
---
# <a name="getncharacterstream-method-int"></a>getNCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，检索指定参数作为 Reader 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.Reader getNCharacterStream(int parameterIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterIndex   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 AReaderobject.  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 当访问**NCHAR**、 **NVARCHAR**和**LONGNVARCHAR**参数时, 应使用此方法。  
  
 此 getNCharacterStream 方法由 getNCharacterStream 方法在 CallableStatement 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [getNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
