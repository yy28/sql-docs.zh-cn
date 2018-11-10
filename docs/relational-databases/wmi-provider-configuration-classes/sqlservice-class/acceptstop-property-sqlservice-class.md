---
title: AcceptStop 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 324df0e451fd2fbdc2986c5f0bc4add86f90eabe
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217325"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于指定是否可以停止服务的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md)表示服务的对象  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定是否可以停止服务： **，则返回 true**如果可以停止该服务，或**false**如果不能停止该服务。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
