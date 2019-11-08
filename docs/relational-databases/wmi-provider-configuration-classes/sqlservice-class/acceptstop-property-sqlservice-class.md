---
title: AcceptStop 属性（SqlService）
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 956151208b93a848219cdac2d897f132511e411d
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659804"
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
 一个表示服务的[SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md)对象  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定是否可以停止服务的布尔值：如果可以停止服务，**则为 true** ; 如果服务无法停止，则为**false** 。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
