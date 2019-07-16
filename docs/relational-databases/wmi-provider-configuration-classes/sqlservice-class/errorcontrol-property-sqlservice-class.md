---
title: ErrorControl 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bad022b2c0a4b2dda7a5de2265c67dd3608b5389
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929680"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取或设置启动期间服务无法启动时的错误严重性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串值，用于指定启动期间服务无法启动时所报告的错误的严重性。 下表列出了可能的值。  
  
 Ignore  
 不通知用户。  
  
 正常  
 通知用户。  
  
 Severe  
 使用上一次已知正确的配置重新启动系统。  
  
 严重  
 系统将尝试使用正确的配置重新启动。  
  
 Unknown  
 严重性未知。  
  
## <a name="remarks"></a>备注  
 此值指示出现故障时启动程序采取的操作。 所有的错误都由计算机系统记录。  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
