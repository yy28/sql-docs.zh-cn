---
title: 更改分区源以使用不同的事实表 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7355f5f7430a5e74cd06ffa73c1b6ed68e11a7c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138101"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>更改分区源以使用不同的事实数据表
  在创建多维数据集的分区时，可以选择使用不同的事实数据表。 不同的数据表可能来自单个数据源视图，也可能来自不同的数据源视图或不同的数据源。 数据源视图也可能包含来自多个数据源的不同表。  
  
 多维数据集分区的所有事实数据表和维度必须与该多维数据集的事实数据表和维度具有相同的结构。 例如，不同的事实数据表可以具有相同结构，同时却包含不同年份或不同产品系列的数据。  
  
 您可以在分区向导的 **“指定源信息”** 页中指定事实数据表。 在该页的 **“查找范围”** 旁边的“分区源”组中，指定要在其中进行查找的数据源或数据源视图。 然后，单击 **“查找表”**，再在 **“可用表”** 下选择要使用的表。  
  
 使用不同的事实数据表时，请确保分区间没有重复的数据。 例如，如果一个事实数据表只包含 2012 年的事务，而另一个事实数据表只包含 2013 年的事务，则二者所包含的数据相互独立。 同样，针对非重复的产品系列或非重复的地域的事实数据表也是相互独立的。  
  
 可以使用包含重复数据的不同事实数据表，但建议不要这样做。 因为在此情况下，您必须在分区中使用筛选器，以确保一个分区使用的数据不被任何其他分区使用。 有关详细信息，请参阅[创建和管理本地分区 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理本地分区&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  