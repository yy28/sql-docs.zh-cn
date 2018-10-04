---
title: AcceptPause 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- AcceptPause Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptPause property
ms.assetid: 4339e903-35ee-4395-b005-ca58b3a24a84
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a0efdc0cf758bf57ea46932e54ccbd7150713483
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173127"
---
# <a name="acceptpause-property-sqlservice-class"></a>AcceptPause 属性（SqlService 类）
  获取用于指定是否可以暂停服务的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.AcceptPause [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定是否可以暂停服务的布尔值属性。 如果可以暂停服务，则为 `true`；如果不能暂停服务，则为 `false`。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
