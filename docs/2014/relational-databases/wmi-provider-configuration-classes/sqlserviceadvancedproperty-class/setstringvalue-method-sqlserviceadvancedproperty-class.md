---
title: SetStringValue 方法 （SqlServiceAdvancedProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SetStringValue Method (SqlServiceAdvancedProperty Class )
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: a02d05f6-1072-4709-9ecc-e23e51c8c898
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9f02ab6929e21c2d4f0d73bfdf55f0cdf18cc67e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076827"
---
# <a name="setstringvalue-method-sqlserviceadvancedproperty-class-"></a>SetStringValue 方法（SqlServiceAdvancedProperty 类）
  设置属性的字符串值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](sqlserviceadvancedproperty-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*strValue*|一个指定高级属性的值的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
 属性值类型必须为`string`以便能够将属性设置为一个字符串值。  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
