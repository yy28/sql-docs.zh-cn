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
manager: craigg
ms.openlocfilehash: 990cb7cccd972ac926824ca3f8d99de3f0d6e305
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687735"
---
# <a name="tostring-method-datetimeoffset"></a>toString 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的字符串表示形式**DateTimeOffset**对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>返回值  
 字符串表示形式**DateTimeOffset**对象。  
  
## <a name="remarks"></a>Remarks  
 字符串具有格式*YYYY*-*MM*-*DD * * hh*:*mm*:*的*[.*fffffff*] [+ |-]*hh*:*mm*。  
  
 返回的字符串的小数部分将用零填充到声明的精度。 例如， **datetimeoffset(6)** 值为"2010年-03-10 12:34:56.78-08:00"作为 DateTimeOffset.toString，从而格式化"2010年-03-10 12:34:56.780000-08:00"。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
