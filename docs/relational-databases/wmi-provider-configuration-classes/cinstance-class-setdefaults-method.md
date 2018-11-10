---
title: SetDefaults 方法 （CInstance 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (CInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: ed9e99c2-3e28-4ee8-bc20-61ca05984973
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9662333176616c9596bda7cc9950a314e7171b01
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217615"
---
# <a name="cinstance-class---setdefaults-method"></a>CInstance 类 - SetDefaults 方法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置实例的所有默认值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选择覆盖现有数据的客户端。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示 [客户端实例的](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) CInstance 类 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*OverwriteAll*|一个布尔值，指定是否覆盖现有值的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端： **true**若要覆盖现有数据，或**false**如果不希望覆盖现有数据。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
