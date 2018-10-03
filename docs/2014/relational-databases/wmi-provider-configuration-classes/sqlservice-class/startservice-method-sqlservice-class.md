---
title: StartService 方法 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- StartService Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 708d96bab30b9828f41b1e29fef80173a6f711aa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098077"
---
# <a name="startservice-method-sqlservice-class"></a>StartService 方法（SqlService 类）
  尝试将服务置于启动状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.StartService()  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定下列启动状态之一的 uint32 值。  
  
 0  
 成功。 已接受该请求。  
  
 1  
 不提供支持。 不支持该请求。  
  
 2  
 拒绝访问。 用户没有相应的访问权限。  
  
 3  
 依赖的服务已运行。 由于其他正在运行的服务依赖于该服务，不能停止该服务。  
  
 4  
 服务控制无效。 请求的控制代码无效或服务无法接受该控制代码。  
  
 5  
 服务无法接受控制。 由于服务的状态 (Win32_BaseService:State) 为 0、1 或 2，无法将请求的控制代码发送到该服务。  
  
 6  
 服务不活动。 该服务尚未启动。  
  
 7  
 服务请求超时。 该服务未及时响应启动请求。  
  
 8  
 未知故障。 启动服务时出现未知故障。  
  
 9  
 找不到路径。 找不到指向服务可执行文件的目录路径。  
  
 10  
 服务已运行。 服务已在运行。  
  
 11  
 服务数据库已锁定。 要添加新服务的数据库已锁定。  
  
 12  
 服务依赖关系已删除。 已从系统中删除此服务依赖的依赖项。  
  
 13  
 服务依赖关系错误。 该服务无法从依赖的服务中找到所需的服务。  
  
 14  
 服务已禁用。 已从系统禁用该服务。  
  
 15  
 服务登录失败。 服务没有在该系统上运行所需的正确身份验证。  
  
 16  
 服务已标记为要删除。 正在从系统删除此服务。  
  
 17  
 服务无线程。 该服务没有执行线程。  
  
 18  
 处于循环依赖关系状态。 启动服务时存在循环依赖关系。  
  
 19  
 处于名称重复状态。 已有一个同名的服务在运行。  
  
 20  
 处于名称无效状态。 该服务的名称中包含无效字符。  
  
 21  
 处于参数无效状态。 向服务传递的参数无效。  
  
 22  
 处于服务帐户无效状态。 用来运行该服务的帐户无效或无权运行该服务。  
  
 23  
 处于服务已存在状态。 系统的服务数据库中已存在该服务。  
  
 24  
 服务已暂停。 该服务目前在系统中已暂停。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
