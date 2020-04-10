---
title: valueOf 方法 (java.sql.Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b32534ac2ace6d2324cb37434c7fe5571159bdde
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919481"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 方法 (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建一个 DateTimeOffset 对象，该对象表示按照距 GMT（给定 java.sql.Timestamp 值以及以分钟指示偏移量的值）的特定偏移量的时间点  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>parameters  
 *timestamp*  
  
 java.sql.Timestamp值。  
  
 minutesOffset   
  
 以分钟表示的偏移量。  
  
## <a name="return-value"></a>返回值  
 返回 DateTimeOffset 对象，表示 java.sql.Timestamp 对象在给定 GMT 偏移（以分钟为单位）处给出的时间点。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
