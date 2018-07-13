---
title: SetStartMode 方法 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetStartMode Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7213e488b13b5b756e8632a55314c0fbbb5a8268
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278803"
---
# <a name="setstartmode-method-sqlservice-class"></a>SetStartMode 方法（SqlService 类）
  修改服务实例的启动模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetStartMode(  
StartMode  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
 *StartMode*  
 一个指定服务实例的启动模式的 `uint32` 值。  
  
 有效值如下：  
  
 值 = 0。 启动 - 设备驱动程序由操作系统加载程序启动。 此值只对驱动程序服务有效。  
  
 值 = 1。 系统 - 设备驱动程序由 `IoInitSystem` 方法启动。 此值只对驱动程序服务有效。  
  
 值 = 2。 自动 - 服务将在系统启动期间由服务控制管理器自动启动。  
  
 值 = 3。 手动 - 服务将在进程调用 `StartService` 方法时由计算机管理器启动。  
  
 值 = 4。 已禁用 - 无法再启动服务。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1。 其他任何数字表示出现错误。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
