---
title: setSendStringParametersAsUnicode 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49198d63-76cb-4843-8d04-e49b1fbb6916
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b630f2bbe44f4484364aa1b99ea987c8888554c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637815"
---
# <a name="setsendstringparametersasunicode-method-sqlserverdatasource"></a>setSendStringParametersAsUnicode 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置指示是否启用以 UNICODE 格式将字符串参数发送到服务器的 boolean 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setSendStringParametersAsUnicode(boolean sendStringParametersAsUnicode)  
```  
  
#### <a name="parameters"></a>Parameters  
 sendStringParametersAsUnicode  
  
 如果以 UNICODE 格式将字符串参数发送到服务器，则为 true。 否则为 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果 sendStringParametersAsUnicode 属性设置为 true（默认值），字符串参数便会以 UNICODE 格式发送到服务器。 如果 sendStringParametersAsUnicode 设置为 false，字符串参数便会以 ASCII/MBCS 格式（而非 UNICODE 格式）发送到服务器。 如果 sendStringParametersAsUnicode 属性未设置，[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md) 返回默认值 true。  
  
 有关 sendStringParametersAsUnicode 连接属性的详细信息，请参阅[连接属性设置](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
