---
description: MDX 数据定义 - REFRESH CUBE
title: " (MDX) 刷新 CUBE 语句 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05ae95c97ae21d3b8ff7b4e457cf3ddf8cc38989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387051"
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
 对于连接到实例的客户端应用程序 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，此语句将导致客户端应用程序上缓存的内存与服务器同步。 但是，通常情况下将对其进行自动检测和更新，这种情况发生之前的时间长度取决于客户端连接字符串的设置。 REFRESH CUBE 语句立即刷新数据。  
  
 对于与本地多维数据集相连的客户端应用程序，REFRESH CUBE 语句导致重新生成本地多维数据集文件。  
  
> [!IMPORTANT]  
>  不能刷新存储在服务器上的命名集。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 数据定义语句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
