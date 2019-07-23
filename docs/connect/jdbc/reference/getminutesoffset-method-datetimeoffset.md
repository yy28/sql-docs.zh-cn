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
ms.openlocfilehash: 6af552920698d4eb149f5edd5ee50128db0e1b61
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981798"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回此 DateTimeOffset 对象的偏移量 (以分钟为单位)。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>返回值  
 以分钟表示的偏移量。  
  
## <a name="remarks"></a>Remarks  
 对于表示8月 2010, 11:35:48-0800 的 DateTimeOffset 对象, getMinutesOffset 返回值480。  
  
## <a name="see-also"></a>另请参阅  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成员](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
