---
title: SetDefaults 方法（SInstance 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDefaults Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDefaults method
ms.assetid: dc3c6a85-0711-4688-bf4f-91168c57af28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ad13821341291a91a989297f29e1459a40de5afe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62720945"
---
# <a name="setdefaults-method-sinstance-class"></a>SetDefaults 方法（SInstance 类）
  设置实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的所有默认值，并提供覆盖现有数据的选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetDefaults(  
OverwriteAll  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务器实例的[SInstance 类](sinstance-class.md)对象。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*OverwriteAll*|一个指定是否覆盖 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端实例的现有值的布尔值：若要覆盖现有值，则为 `true`；如果不希望覆盖现有值，则为 `false`。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
