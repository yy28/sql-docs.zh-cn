---
title: getMinutesOffset 方法 (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d17b5451340c07ea8c9bd0ce61bf858b419b121
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784760"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在几分钟内从格林威治标准时间，此 DateTimeOffset 对象中返回的偏移量。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>返回值  
 以分钟表示的偏移量。  
  
## <a name="remarks"></a>Remarks  
 对于 DateTimeOffset 对象，表示 8 2010 年 3 月，11:35:48-0800，getMinutesOffset 返回值 480。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
