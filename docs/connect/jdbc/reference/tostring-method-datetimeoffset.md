---
description: toString 方法 (DateTimeOffset)
title: toString 方法 (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66931c3ada32b112de920aab3ac62fdb50fd40cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431429"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回 DateTimeOffset**** 对象的字符串表示形式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>返回值  
 DateTimeOffset**** 对象的字符串表示形式。  
  
## <a name="remarks"></a>注解  
 此字符串格式为 `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`。  
  
 返回的字符串的小数部分将用零填充到声明的精度。 例如，值为“2010-03-10 12:34:56.78 -08:00”的 datetimeoffset(6)**** 的格式设置中，DateTimeOffset.toString 设置为“2010-03-10 12:34:56.780000 -08:00”。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
