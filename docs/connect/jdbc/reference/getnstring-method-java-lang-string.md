---
title: getNString 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 118025da1121f3e6c04fd17074dd3b2df53e9c26
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80905343"
---
# <a name="getnstring-method-javalangstring"></a>getNString 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定 NCHAR  、NVARCHAR  或 LONGNVARCHAR  参数的值作为 Java 编程语言中的 String 进行检索。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>parameters  
 parameterName   
  
 包含参数名称的字符串  。  
  
## <a name="return-value"></a>返回值  
 AStringobject。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getNString 方法是由 java.sql.CallableStatement 接口中的 getNString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getNString 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 方法](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
