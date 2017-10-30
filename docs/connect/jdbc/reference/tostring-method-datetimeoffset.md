---
title: "toString 方法 (DateTimeOffset) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b0c31538c7260b81a88822099f56a05b70a0a96
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>注释  
 字符串具有格式*YYYY*-*MM*-*DD**hh*:*mm*:*ss*[。*fffffff*] [+ |-]*hh*:*mm*。  
  
 返回的字符串的小数部分将用零填充到声明的精度。 例如， **datetimeoffset(6)**值为"2010年-03-10 12:34:56.78-08:00"将设置格式的作为 DateTimeOffset.toString"2010年-03-10 12:34:56.780000-08:00"。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

