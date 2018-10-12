---
title: setNString 方法 （int，java.lang.String） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7da6d44-f5b1-44f8-95f5-40179968b1b0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cef8c88654cf29f9a860a30fc3b79ef6d5124ce4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650015"
---
# <a name="setnstring-method-int-javalangstring"></a>setNString 方法 (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的 String 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNString(int parameterIndex,  
                                                  java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 指示参数索引的 int。  
  
 *value*  
  
 包含参数值的 String 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此方法应用于**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**数据类型。  
  
 此 setNString 方法是由 java.sql.PreparedStatement 接口中的 setNString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
