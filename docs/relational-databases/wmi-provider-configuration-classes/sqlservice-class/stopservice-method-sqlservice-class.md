---
description: StopService 方法（SqlService 类）
title: 'StopService 方法 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StopService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StopService method
ms.assetid: ef8e1856-4930-417a-8f52-be470fd3f15c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7f4c01a00f1ce264cc26ebbfd7f4ad6a682e5ba6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485090"
---
# <a name="stopservice-method-sqlservice-class"></a>StopService 方法（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  尝试将服务置于停止状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.StopService()  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果已接受 **ResumeService** 请求，则为 0；如果不支持该请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
