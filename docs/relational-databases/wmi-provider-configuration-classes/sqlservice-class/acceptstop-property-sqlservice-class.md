---
title: "AcceptStop 属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7790ad93e9eaf06374b5520a196c924f38d6d84
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于指定是否可以停止服务的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md)表示服务的对象  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定是否可以停止该服务： **true**如果可以停止该服务，或**false**如果不停止该服务。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
