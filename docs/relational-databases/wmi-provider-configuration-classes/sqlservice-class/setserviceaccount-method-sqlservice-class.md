---
description: SetServiceAccount 方法（SqlService 类）
title: 'SetServiceAccount 方法 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbd892624ec888635439d19311d9ba823ee52c98
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89519945"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount 方法（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  尝试更改运行服务实例时使用的用户名和密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
#### <a name="parameters"></a>参数  
 *ServiceStartName*  
 一个指定运行服务所用帐户名的字符串值。 根据不同的服务类型，帐户名可能的格式为“域名\用户名”。 服务进程运行时，将使用以下两种格式之一登录：  
  
-   如果帐户属于内置域，则可以指定“\用户名”。  
  
-   如果指定 NULL，则该服务将作为 **LocalSystem** 帐户登录。  
  
 对于内核或系统级驱动程序， *StartName* 包含驱动程序对象名称（\FileSystem\Rdr 或 \Driver\Xns），i/o 系统使用该名称加载设备驱动程序。 如果指定 NULL，驱动程序将以 I/O 系统基于服务名称创建的默认对象名称运行，例如 DWDOM\Admin。  
  
 *ServiceStartPassword*  
 一个字符串值，该值指定 *StartName* 参数中的帐户名称的密码。 如果不更改密码，请指定 NULL。 如果服务没有密码，请指定一个空字符串。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1。 其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
