---
title: Size 属性（ClientNetLibInfo）
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Size Property (ClientNetLibInfo Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Size property
ms.assetid: 66f7264e-2c18-40f5-8091-b5dd83d5716f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9f7aa3059a6c67e236aa5b64fbc564addc62f586
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731460"
---
# <a name="size-property-clientnetlibinfo-class"></a>Size 属性（ClientNetLibInfo 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  获取客户端网络库文件的大小 (KB)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Size [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示有关客户端网络库的信息的 [ClientNetLibInfo 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetlibinfo-class/clientnetlibinfo-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络库文件的大小的 uint32 值 (KB)。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
