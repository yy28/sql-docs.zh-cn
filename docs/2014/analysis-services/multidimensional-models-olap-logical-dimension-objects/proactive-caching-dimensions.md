---
title: 主动缓存 （维度） |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f5e6bab81e982adbf8ee443bd84a5e806b960db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727292"
---
# <a name="proactive-caching-dimensions"></a>主动缓存（维度）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以利用主动缓存自动创建 MOLAP 缓存以及管理 OLAP 对象。 多维数据集可利用收自数据库的通知，立即合并对数据库中数据所做的更改。 主动缓存的目标是提供传统 MOLAP 所具有的性能，并同时保持使用 ROLAP 进行管理所具有的方便和快捷。  
  
 简单 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象由计时规范和表通知组成。 计时规范定义收到更改通知后更新缓存的时间范围。 表通知定义数据表和 <xref:Microsoft.AnalysisServices.ProactiveCaching> 对象之间的通知架构。  
  
  
