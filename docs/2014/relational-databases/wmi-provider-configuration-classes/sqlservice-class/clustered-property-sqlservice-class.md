---
title: Clustered 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- Clustered Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ca448090841c06d208c64f6ff483cc5cdb8473
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079899"
---
# <a name="clustered-property-sqlservice-class"></a>Clustered 属性（SqlService 类）
  获取用于指定服务是否是群集实例的一部分的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Clustered [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务是否参与群集实例的布尔值：如果服务参与群集实例，则为 `true`；如果服务不参与群集实例，则为 `false`。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
