---
title: IsReadOnly 属性（SqlServiceAdvancedProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- IsReadOnly Property (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- IsReadOnly property
ms.assetid: 9672e70f-1d8c-4133-ac73-3b5733a1c4ee
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 84e742a04dc3a019e27818e921beb694ca77b9af
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061301"
---
# <a name="isreadonly-property-sqlserviceadvancedproperty-class"></a>IsReadOnly 属性（SqlServiceAdvancedProperty 类）
  获取或设置用于指定高级属性是否为只读的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.IsReadOnly [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](sqlserviceadvancedproperty-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定高级属性是否为只读的布尔值：如果高级属性为只读，则为 `true`；如果高级属性可以修改，则为 `false`。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
