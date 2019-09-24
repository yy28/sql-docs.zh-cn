---
title: toString 方法 (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3acffe6a922084fd63e38a8e212b5cf86d6b278
ms.sourcegitcommit: c0fd28306a3b42895c2ab673734fbae2b56f9291
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71096909"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**DateTimeOffset**对象的字符串表示形式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>返回值  
 **DateTimeOffset**对象的字符串表示形式。  
  
## <a name="remarks"></a>Remarks  
 此字符串格式为 `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`。  
  
 返回的字符串的小数部分将用零填充到声明的精度。 例如, 值为 "2010-03-10 12:34: 08:00 56.78" 的**datetimeoffset (6)** 将由 datetimeoffset 格式设置为 "2010-03-10 12:34: 56.780000-08:00"。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
