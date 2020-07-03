---
title: IsReadOnly 属性（SqlServiceAdvancedProperty）
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IsReadOnly Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IsReadOnly property
ms.assetid: 9672e70f-1d8c-4133-ac73-3b5733a1c4ee
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 031ffc6a0efc9a339ca40a83aee14e73d0c91d8d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880541"
---
# <a name="isreadonly-property-sqlserviceadvancedproperty-class"></a>IsReadOnly 属性（SqlServiceAdvancedProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取或设置用于指定高级属性是否为只读的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.IsReadOnly [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定高级属性是否为只读的布尔值：如果高级属性为只读，则为 **true** ；如果高级属性可以修改，则为 **false** 。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
