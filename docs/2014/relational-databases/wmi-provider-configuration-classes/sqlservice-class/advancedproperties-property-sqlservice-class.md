---
title: AdvancedProperties 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- AdvancedProperties Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AdvancedProperties property
ms.assetid: 63bcb7e2-1f78-4961-b4b9-1b635a89079b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 83cee30cb86c28933e3a86a9e8a75e8dc3c4f71a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138409"
---
# <a name="advancedproperties-property-sqlservice-class"></a>AdvancedProperties 属性（SqlService 类）
  获取一组包含 `SqlService` 对象的高级属性的对象引用。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.AdvancedProperties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个数组[SqlServiceAdvancedProperty 类](../sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md)包含的高级的属性的对象`SqlService`对象。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
