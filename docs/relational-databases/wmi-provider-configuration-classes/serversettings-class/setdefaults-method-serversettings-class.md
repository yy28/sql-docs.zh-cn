---
title: SetDefaults 方法（ServerSettings）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86e15376bd56a439e0763e79a5c166d7023125ea
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660273"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 方法（ServerSettings 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  为 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例设置所有默认值，并选择覆盖现有数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端实例的[ServerSettings 类](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)对象。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|说明|  
|---------------|-----------------|  
|*OverwriteAll*|一个布尔值，指定是否覆盖 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的实例上的现有值： **true**以覆盖现有数据，如果不覆盖现有数据，则为**false** 。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 u**int32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
