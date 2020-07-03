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
ms.openlocfilehash: 4c1f7670aa0e90f848c3f66e65df104181541dee
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880726"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 方法（ServerSettings 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  设置实例的所有默认值， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并提供覆盖现有数据的选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示客户端实例的[ServerSettings 类](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md)对象 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*OverwriteAll*|指定是否覆盖实例上的现有值的布尔值 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ：如果要覆盖现有数据，则为**true** ; 否则为**false** 。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 U**int32**值，如果服务已成功修改，则为 0; 如果不支持该请求，则为 1; 其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
