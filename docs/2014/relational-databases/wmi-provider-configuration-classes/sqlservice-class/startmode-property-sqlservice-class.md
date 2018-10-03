---
title: StartMode 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: dbdf2e807f5f36cf8814be95cb98ec53bb813790
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128433"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 属性（SqlService 类）
  获取服务的启动模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务模式的 uint32 值。  
  
 可以是下列值之一。  
  
 启动  
 值 = 0。 服务由操作系统加载程序启动。 此选项只对驱动程序服务有效。  
  
 系统  
 值 = 1。 服务由 `IoInitSystem` 方法启动。 此选项只对驱动程序服务有效。  
  
 自动  
 值 = 2。 服务将在系统启动期间由服务控制管理器自动启动。  
  
 Manual  
 值 = 3。 服务将在进程调用 `StartService` 方法时由计算机管理器启动。  
  
 禁用  
 值 = 4。 无法启动服务。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
