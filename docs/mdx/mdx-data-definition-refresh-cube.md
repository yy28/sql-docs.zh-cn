---
title: REFRESH CUBE 语句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dafc13dda1f8ecab1400a88d1ca66eff5f317e43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63285074"
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 数据定义 - REFRESH CUBE


  刷新多维数据集的客户端缓存。  
  
## <a name="syntax"></a>语法  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 客户端应用程序连接到的实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，此语句导致缓存客户端应用程序与服务器同步的内存。 但是，通常情况下将对其进行自动检测和更新，这种情况发生之前的时间长度取决于客户端连接字符串的设置。 REFRESH CUBE 语句立即刷新数据。  
  
 对于与本地多维数据集相连的客户端应用程序，REFRESH CUBE 语句导致重新生成本地多维数据集文件。  
  
> [!IMPORTANT]  
>  不能刷新存储在服务器上的命名集。  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
