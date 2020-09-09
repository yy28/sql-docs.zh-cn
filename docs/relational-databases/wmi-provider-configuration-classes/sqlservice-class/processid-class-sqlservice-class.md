---
description: ProcessId 类（SqlService 类）
title: 'ProcessId 类 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProcessId Class (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d4e6ceb18ecda885481860bf9889143bccfd0ed6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539998"
---
# <a name="processid-class-sqlservice-class"></a>ProcessId 类（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取唯一标识服务的系统进程 ID。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProcessId [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，指定唯一标识进程的 ID。  
  
## <a name="remarks"></a>备注  
  
## <a name="example"></a>示例  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
