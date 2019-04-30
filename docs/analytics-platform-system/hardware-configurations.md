---
title: 硬件配置的分析平台系统 |Microsoft Docs
description: Analytics Platform System (APS) 设备硬件配置有可缩放单位，以便根据你的业务要求购买适当数量的处理和存储。 设备会存储有关并行数据仓库从几兆兆字节到超过 6 拍字节的数据。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2a252e5f2aebd8d51b9b0eb1f353ded504155c2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283279"
---
# <a name="hardware-configurations---analytics-platform-system"></a>硬件配置的分析平台系统
Analytics Platform System (APS) 硬件构建方式，以便根据你的业务要求购买适当数量的处理和存储可缩放单位。 设备可缩放存储的 SQL Server 并行数据仓库 (PDW) 从几兆兆字节到超过 6 拍字节的数据。  
  
## <a name="contents"></a>目录  
  
-   [一个机架配置](#section1)  
  
-   [多机架配置](#section2)  

  
## <a name="section1"></a>一个机架配置  
在装置中的第一个机架包含运行 PDW 所需的组件。 机架和网络以及一个基本的缩放单位，最小设备配置。 这些图显示方式，可以配置第一个设备的机架。 您可以在第一个机架，具体取决于硬件供应商中的 2 到 9 计算节点之间。  
  
### <a name="first-rack-configurations---dell"></a>第一次机架配置-DELL  
DELL 设备的最小配置具有 3 个计算节点。 可以将最多 2 个数据扩展单元添加到第一个机架总共 9 个计算节点。  
  
![Dell 第一机架配置](media/first-rack-configurations-dell.png "Dell 第一机架配置")  
  
### <a name="first-rack-configurations---hpe"></a>首次安装机架配置-HPE  
HPE 设备的最小配置具有 2 个计算节点。 可以将最多 3 个数据扩展单元添加到共 8 个计算节点的第一个机架中。  
  
![HPE 首先机架配置 HPE](media/first-rack-configurations-hpe.png "HPE 首先机架配置")  
  
## <a name="section2"></a>多机架配置  
若要将容量添加到 PDW 可以添加网络、 数据缩放单位，以及根据需要提供正确的强大功能，其他机架和网络组件并机架基础结构。 每个其他的机架和网络要求被动主机。  
  
每个硬件供应商指定数据缩放单位可以添加给定的容量的设备的数。 我们建议添加足够的数据缩放单位，以查看至少 20%提升性能。 例如，添加一个数据规模单位到已有 20 个数据缩放单位的设备可能会导致可忽略不计的性能提升。 净的性能收益不值得的成本和人力。  
  
### <a name="scale-out-example---hpe"></a>横向扩展示例-HPE  
下图显示了一个包含 20 个计算节点的 3 个机架 HP 设备。  
  
![有 20 个计算节点的 HPE 装置](media/scale-out-hpe.png "HPE 设备，但 20 个计算节点")  
  
### <a name="scale-out-example---dell-quanta"></a>横向扩展示例-DELL，量程  
下图显示了包含 21 的计算节点的 3 个机架 DELL 或 Quanta 设备。  
  
![Dell 设备，但 21 的计算节点](media/scale-out-dell.png "Dell 设备，但 21 的计算节点")  
 
