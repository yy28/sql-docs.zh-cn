---
title: valueOf 方法 （java.sql.Timestamp，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ced75c886fcc0bf58d1671e50a213d5a6003a97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704096"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 方法 (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建一个 DateTimeOffset 对象，该对象表示按照距 GMT（给定 java.sql.Timestamp 值以及以分钟指示偏移量的值）的特定偏移量的时间点。  
  
## <a name="syntax"></a>语法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parameters  
 *timestamp*  
  
 java.sql.Timestamp值。  
  
 *minutesOffset*  
  
 以分钟表示的偏移量。  
  
## <a name="return-value"></a>返回值  
 返回 DateTimeOffset 对象表示的由给定的偏移量处的 java.sql.Timestamp 对象中给定分钟，按照距 GMT 的时间点。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
