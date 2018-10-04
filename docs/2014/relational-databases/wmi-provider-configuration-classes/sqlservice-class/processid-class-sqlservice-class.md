---
title: ProcessId 类 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2bcc9e31fd70f0201f26751bddbcb3f3f8aeec98
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080917"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 类（SqlService 类）
  获取唯一标识服务的系统进程 ID。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定唯一标识进程的 `uint32` 值。  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
