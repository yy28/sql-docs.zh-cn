---
title: setSendTimeAsDatetime 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad4f7e8cee834619985be1ab140bc39698215060
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798235"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此方法。  
  
 将修改的设置**sendTimeAsDatetime**连接属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sendTimeAsDateTime*  
  
 一个布尔值。 如果设置为 true，java.sql.Time 值将作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 类型发送到服务器。 如果设置为 false，java.sql.Time 值将作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] time 类型发送到服务器。  
  
## <a name="remarks"></a>Remarks  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) 返回“sendTimeAsDatetime”连接属性的设置。  
  
 有关详细信息**sendTimeAsDatetime**连接属性，请参阅[设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
