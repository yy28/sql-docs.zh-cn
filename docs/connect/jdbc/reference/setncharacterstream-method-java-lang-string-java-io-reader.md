---
description: setNCharacterStream 方法 (java.lang.String, java.io.Reader)
title: 设置为 Reader 对象的 setNCharacterStream 方法 - string | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94f5ca83d56eb168d2a89b425c7a24a0b4351d72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431639"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>setNCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>参数  
 parameterName  
  
 指示参数名称的字符串****。  
  
 *value*  
  
 Reader 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setNCharacterStream 方法是由 java.sql.CallableStatement 接口中的 setNCharacterStream 方法指定的。  
  
 此方法应用于 NCHAR****、NVARCHAR****、NTEXT**** 和 XML**** 数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [setNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
