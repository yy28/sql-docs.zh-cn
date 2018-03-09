---
title: "SetServiceAccount 方法 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bdcb3f6789baf009165a74bcf3d82630fa868fd
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount 方法（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
尝试更改运行服务实例时使用的用户名和密码。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
 *ServiceStartName*  
 一个指定运行服务所用帐户名的字符串值。 根据不同的服务类型，帐户名可能的格式为“域名\用户名”。 服务进程运行时，将使用以下两种格式之一登录：  
  
-   如果帐户属于内置域，则可以指定“\用户名”。  
  
-   如果指定 NULL，则服务将记录为**LocalSystem**帐户。  
  
 内核或系统级的驱动程序， *StartName*包含驱动程序对象名称，\FileSystem\Rdr 或 \Driver\Xns，I/O 系统用来加载设备驱动程序。 如果指定 NULL，驱动程序将以 I/O 系统基于服务名称创建的默认对象名称运行，例如 DWDOM\Admin。  
  
 *ServiceStartPassword*  
 一个字符串值，指定的密码中的帐户名称*StartName*参数。 如果不更改密码，请指定 NULL。 如果服务没有密码，请指定一个空字符串。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1。 其他任何数字表示出现错误。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
