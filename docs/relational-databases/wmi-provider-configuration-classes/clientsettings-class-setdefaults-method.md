---
title: SetDefaults 方法 （ClientSettings 类） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bedc2c0b326b0007c3a4d3edbc6301090fd709d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="clientsettings-class---setdefaults-method"></a>ClientSettings 类-SetDefaults 方法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置的实例的所有默认值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项覆盖现有数据的客户端。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A **ClientSettings**对象，表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端实例。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*OverwriteAll*|一个指定是否覆盖 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端实例的现有值的布尔值。 **true**覆盖现有数据;**false**如果现有的数据是不被覆盖。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
