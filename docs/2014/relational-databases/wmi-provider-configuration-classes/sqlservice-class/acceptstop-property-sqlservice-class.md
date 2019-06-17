---
title: AcceptStop 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- AcceptStop Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 38da38f867c6266d25f3b5d4c329a3e18a0e7292
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63223338"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 属性（SqlService 类）
  获取用于指定是否可以停止服务的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.AcceptStop [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个[SqlService 类](sqlservice-class.md)表示服务的对象  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定是否可以停止服务的布尔值属性。如果可以停止服务，则为 `true`；如果不能停止服务，则为 `false`。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
