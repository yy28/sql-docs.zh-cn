---
title: "刷新多维数据集语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- REFRESH CUBE
- REFRESH_CUBE
- REFRESH
dev_langs: kbMDX
helpviewer_keywords:
- cubes [Analysis Services], cache
- refreshing cache
- REFRESH CUBE statement
- cache [Analysis Services]
ms.assetid: b8c087fb-5d17-4b13-b7cf-9929e9aab35c
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2656c588a90ce68f916815be28d157f1a51e0e23
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---refresh-cube"></a>MDX 数据定义的刷新多维数据集
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刷新多维数据集的客户端缓存。  
  
## <a name="syntax"></a>语法  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串表达式。  
  
## <a name="remarks"></a>注释  
 客户端应用程序连接到的实例[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，此语句会导致在客户端应用程序与服务器同步上缓存的内存。 但是，通常情况下将对其进行自动检测和更新，这种情况发生之前的时间长度取决于客户端连接字符串的设置。 REFRESH CUBE 语句立即刷新数据。  
  
 对于与本地多维数据集相连的客户端应用程序，REFRESH CUBE 语句导致重新生成本地多维数据集文件。  
  
> [!IMPORTANT]  
>  不能刷新存储在服务器上的命名集。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
