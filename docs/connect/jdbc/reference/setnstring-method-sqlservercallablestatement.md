---
title: setNString 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 690f4e43fcbc1064fe0e59143be76d24e5cfc556
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800345"
---
# <a name="setnstring-method-sqlservercallablestatement"></a>setNString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的 String 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName   
  
 指示参数名称的字符串  。  
  
 *value*  
  
 一个字符串对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此方法应用于**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**数据类型。  
  
 此 setNString 方法是由 java.sql.CallableStatement 接口中的 setNString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
