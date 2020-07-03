---
title: SetNumValue 方法（SqlServiceAdvancedProperty）
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumValue method
ms.assetid: a5e1056b-0b75-4ad6-99c1-89246010d815
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 619b06f1279c36716538535050b4e2795724dad7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888292"
---
# <a name="setnumvalue-method-sqlserviceadvancedproperty-class"></a>SetNumValue 方法（SqlServiceAdvancedProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  设置属性的数值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetNumValue(NumValue)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 对象。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*NumValue*|一个指定高级属性的值的 **uint32** 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
 属性值类型必须为 Numeric，才能将属性设置为数值。  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
