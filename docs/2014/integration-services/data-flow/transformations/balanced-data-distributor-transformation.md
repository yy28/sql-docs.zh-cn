---
title: 平衡数据分发器转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.balanceddatadistributor.f1
ms.assetid: ae0b33dd-f44b-42df-b6f6-69861770ce10
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 175f52195a20c965915e1d144f661f53fbb42573
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187104"
---
# <a name="balanced-data-distributor-transformation"></a>平衡的数据分发服务器转换
  平衡的数据分发服务器 (BDD) 转换可利用新型 CPU 的并发处理能力。 它可将传入行的缓冲区均匀分布到各个独立线程的输出上。 通过对每个输出路径使用独立线程，BDD 组件提升了运行在多核和多处理器服务器上的 SSIS 包的性能。 BDD 组件是 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能包的一部分。 下载并安装它从[此处](http://go.microsoft.com/fwlink/p/?LinkId=391999)。  
  
 下图展示了一个使用 BDD 转换的简单示例。 在该示例中，BDD 转换从平面文件源的输入数据中每次挑选一个管道缓冲区并以循环方式将其向下发送至三个输出路径之一。 在 SQL Server Data Tools 中显示数据流任务属性的“属性”窗口中，可查看 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferSize%2A>（管道缓冲区默认大小）和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferMaxRows%2A>（管道缓冲区默认最大行数）的值。  
  
 ![平衡数据分发器](../../media/balanceddatadistributor.JPG "Balanced Data Distributor")  
  
 平衡的数据分发服务器转换可在满足以下条件的方案中提升包的性能：  
  
1.  有大量数据传入 BDD 转换。 如果数据大小较小且只有一个缓冲区能够存放数据，则使用 BDD 转换没有任何意义。 如果数据大小较大且需要多个缓冲区来存放数据，则 BDD 能够借助独立线程高效地并行处理数据缓冲区。  
  
2.  数据的读取速度可能会超过数据流其余部分处理数据的速度。 在这种情况下，在数据上执行的转换的运行速度将慢于数据的传入速度。 如果瓶颈出在目标处，则该目标必须是可并行化的。  
  
3.  数据不必有序。 例如，若要使数据保持有序，则不应使用 BDD 转换来拆分数据。  
  
 请注意，如果 SSIS 包中的瓶颈在于从源读取数据的速度，则 BDD 组件无助于性能的提高。 如果 SSIS 包中的瓶颈是因为目标不支持并行，则 BDD 爱莫能助；但是，可以并行执行所有转换并使用 Union All 转换将来自不同 BDD 转换输出路径的输出数据合并，然后再将数据发送至目标。  
  
> [!IMPORTANT]  
>  有关使用该转换的演示，请观看 TechNet Library 上 [平衡的数据分发服务器视频](http://go.microsoft.com/fwlink/?LinkID=226278) 。  
  
  
