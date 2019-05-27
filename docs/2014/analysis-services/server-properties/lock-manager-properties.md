---
title: 锁管理器属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- lock manager properties [Analysis Services]
- LockWaitGranularityMS property
- DefaultLockTimeoutMS property
- DeadlockDetectionGranularityMS property
ms.assetid: 15fe9ead-825b-4ac3-9191-7a07caa2861b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 607654924a9f7e2d071bbce1ee4797792cb760c9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068942"
---
# <a name="lock-manager-properties"></a>锁管理器属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的锁管理器服务器属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
 **适用范围：** 多维和表格服务器模式  
  
## <a name="properties"></a>属性  
 `DefaultLockTimeoutMS`  
 有符号 32 位整数属性，用于定义内部锁请求的默认锁超时值（毫秒）。  
  
 该属性的默认值为 -1，指示没有为内部锁请求指定超时值。  
  
 `LockWaitGranularityMS`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `DeadlockDetectionGranularityMS`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
