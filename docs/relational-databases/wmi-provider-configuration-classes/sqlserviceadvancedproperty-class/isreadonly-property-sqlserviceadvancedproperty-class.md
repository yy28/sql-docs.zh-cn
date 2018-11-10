---
title: IsReadOnly 属性 （SqlServiceAdvancedProperty 类） |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 74fbaeaf5cd73c2fc43dccd99f1db6cadc4262f2
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217485"
---
# <a name="isreadonly-property-sqlserviceadvancedproperty-class"></a>IsReadOnly 属性（SqlServiceAdvancedProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取或设置用于指定高级属性是否为只读的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.IsReadOnly [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示高级属性的 [SqlServiceAdvancedProperty 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定高级属性是否为只读的布尔值：如果高级属性为只读，则为 **true** ；如果高级属性可以修改，则为 **false** 。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
