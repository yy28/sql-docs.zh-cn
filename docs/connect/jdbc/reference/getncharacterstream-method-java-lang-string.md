---
title: getNCharacterStream 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0dd13d292aaade59348a7673e56c4beaa59865a9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80905917"
---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数作为 Reader 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>parameters  
 columnLabel   
  
 一个包含列标签的字符串  。  
  
## <a name="return-value"></a>返回值  
 Reader 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 访问 NCHAR  、NVARCHAR  和 LONGNVARCHAR  参数时，应使用此方法。  
  
 此 getNCharacterStream 方法是由 java.sql.CallableStatement 接口中的 getNCharacterStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
