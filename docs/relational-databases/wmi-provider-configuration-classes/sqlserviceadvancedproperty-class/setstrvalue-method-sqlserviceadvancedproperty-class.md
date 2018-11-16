---
title: SetStrValue 方法 （SqlServiceAdvancedProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStrValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStrValue method
ms.assetid: 1fededc3-81ba-4b08-83f9-189b96140799
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f2e65b3b8f1e0a2a98de7a676bd7e1571ad24e46
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666067"
---
# <a name="setstrvalue-method-sqlserviceadvancedproperty-class"></a>SetStrValue 方法（SqlServiceAdvancedProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置属性的字符串值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*strValue*|一个指定高级属性的值的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
 属性值类型必须为 *string* ，才能将属性设置为字符串值。  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
