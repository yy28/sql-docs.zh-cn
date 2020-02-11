---
title: 硬件配置
description: 分析平台系统（AP）设备硬件是利用可缩放的单元构建的，因此，你可以根据业务需求购买适当数量的处理和存储。 设备可将并行数据仓库的存储从数 tb 扩展到超过 6 pb 的数据。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401136"
---
# <a name="hardware-configurations---analytics-platform-system"></a>硬件配置-分析平台系统
分析平台系统（AP）硬件是通过可缩放的单元构建的，因此，你可以根据业务需求购买适当数量的处理和存储。 该设备将 SQL Server Parallel Data 仓库（PDW）的存储从数 Tb 扩展到超过 6 Pb 的数据。  
  
## <a name="contents"></a>目录  
  
-   [一架式配置](#section1)  
  
-   [多机架配置](#section2)  

  
## <a name="section1"></a>一架式配置  
设备中的第一个机架包含运行 PDW 所需的组件。 最小设备配置为机架，网络加上基本缩放单位。 这些关系图显示了设备的第一个机架的配置方法。 在第一个机架中可以有2到9个计算节点，具体取决于硬件供应商。  
  
### <a name="first-rack-configurations---dell"></a>第一机架配置-DELL  
DELL 设备的最低配置具有3个计算节点。 最多可以向第一个货架添加2个数据缩放单位，总计9个计算节点。  
  
![Dell 第一机架配置](media/first-rack-configurations-dell.png "Dell 第一机架配置")  
  
### <a name="first-rack-configurations---hpe"></a>第一机架配置-HPE  
HPE 设备的最低配置具有2个计算节点。 最多可以向第一个机架添加3个数据缩放单位，总共8个计算节点。  
  
![HPE 的 HPE 第一架配置](media/first-rack-configurations-hpe.png "HPE 第一架配置")  
  
## <a name="section2"></a>多机架配置  
若要将容量添加到 PDW，你可以根据需要添加数据扩展单元和其他机架 & 网络组件，以提供正确的电源、网络和机架基础结构。 每个额外机架 & 网络都需要被动主机。  
  
每个硬件供应商指定你可以为你的设备的容量增加的数据缩放单位数。 建议添加足够多的数据缩放单位，以查看性能提升的20%。 例如，将一个数据缩放单元添加到已经具有20个数据缩放单位的设备可能会导致性能提高。 净收益并不值得成本和精力。  
  
### <a name="scale-out-example---hpe"></a>Scale out 示例-HPE  
此图显示了3个机架 HP 设备，其中包含20个计算节点。  
  
![具有20个计算节点的 HPE 设备](media/scale-out-hpe.png "具有20个计算节点的 HPE 设备")  
  
### <a name="scale-out-example---dell-quanta"></a>Scale Out 示例-DELL、量程  
此图显示了3个机架，其中包含21个计算节点。  
  
![具有21个计算节点的戴尔设备](media/scale-out-dell.png "具有21个计算节点的戴尔设备")  
 
