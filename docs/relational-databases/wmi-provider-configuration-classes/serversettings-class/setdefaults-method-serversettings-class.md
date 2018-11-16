---
title: SetDefaults 方法 （ServerSettings 类） |Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 5e7a9dfd6d68f25b98469a79850444fc4726d785
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668076"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 方法（ServerSettings 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置实例的所有默认值[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]覆盖现有数据的选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerSettings 类](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端实例。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*OverwriteAll*|一个布尔值，指定是否覆盖现有值的实例上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: **true**若要覆盖现有数据，或**false**如果不希望覆盖现有数据。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 u**int32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
