---
title: 硬件组件的分析平台系统 |Microsoft Docs
description: Analytics Platform System (APS) 使用可扩展的组件，因此您可以根据你的业务要求购买适当数量的处理和存储。 如果您订购 AP，将需要这些核心硬件组件的组合。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0f7f3bd8f4d5500a59675d40ff7f50d1afd9a199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960881"
---
# <a name="hardware-components-for-analytics-platform-system"></a>分析平台系统的硬件组件

Analytics Platform System (APS) 使用可扩展的组件，因此您可以根据你的业务要求购买适当数量的处理和存储。 如果您订购 AP，将需要这些核心硬件组件的组合。 特定的硬件供应商可能使用不同的命名约定或其他组件。  
 
  
## <a name="rackandnetwork"></a>机架和网络 
 
APS 组件都存储在你的数据中心中显示的一个或多个机架。 每个机架附带了配电装置 (Pdu)、 两个 InfiniBand 交换机和两个以太网交换机。  
  
![机架和网络](media/rack-and-network.png "APS 机架和网络")  
  
## <a name="datascaleunit"></a>数据缩放单位
 
数据缩放单位包含的数据的主机和直连的存储 (DAS) 来处理和存储用户数据。 若要增加容量将添加数据缩放单位根据支持的硬件供应商的配置。 随着数据规模单位数的增长，您需要添加其他机架和网络组件，根据需要，提供更大电源、 网络和机架基础结构。  
  
### <a name="data-host"></a>数据主机  

数据主机是专用服务器来处理用户数据。 并行数据仓库 (PDW) 在每个数据主机上运行一个计算节点。 对于 HPE 设备的数据缩放单位具有数据的两个主机。 Dell 和量程装置，数据规模单位都具有三个主机中的数据。  
  
### <a name="direct-attached-storage"></a>直接附加的存储
 
直连的存储 (DAS) 是连接到数据主机磁盘的池。 所有数据主机可以访问的任何磁盘。 作为一部分无共享体系结构，在数据的主机上运行的计算节点不共享单个磁盘。 但是，以实现高可用性，共享存储访问，并且每个数据主机可以访问的任何磁盘。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>数据规模单元体系结构-DELL 和量程
  
![可伸缩性单元](media/scalability-unit-dell.png "Dell 的可伸缩性单元")  
  
### <a name="data-scale-unit-architecture---hpe"></a>数据规模单元体系结构-HPE 
 
![HPE 可伸缩性单元](media/scalability-unit-hpe.png "HPE 可伸缩性单元")  
  
### <a name="data-scale-unit-description"></a>数据规模单元描述

数据缩放单位为每个计算节点和一个直连磁盘阵列使用串行连接 SCSI (SAS) 附加有一台服务器 （主机）。 中的 cab 文件的存储，磁盘阵列分为两个部分，每个包含冗余电源。 Windows Server 存储空间管理用户数据的方法在 RAID 1 镜像的磁盘对之间复制数据。 在每个磁盘对磁盘存储在磁盘阵列的不同部分。  
  
磁盘阵列还包含热备用磁盘和系统磁盘。 如果磁盘发生故障时，存储空间使用正确的副本的数据磁盘上的正常运行以重新生成上的热备用的数据的重复副本。 这是一个重要的自修复功能，以帮助防止数据丢失。  
  
为计算节点的磁盘总数：  
  
-   DELL 有 96 磁盘 = （3 个服务器） * （每个服务器的 16 个磁盘） \* (冗余磁盘为 2 个)。  
  
-   HPE 具有 64 个磁盘 = （2 个服务器） * （每个服务器的 16 个磁盘） \* (冗余磁盘为 2 个)。  
  
-   此外，每个磁盘阵列具有热备用磁盘和系统磁盘。  
  
**为实现高可用性**，当计算节点进行故障转移，它可以仍然有效，并通过在数据缩放单位中的其他主机访问其用户数据。 至少一个直接连接的物理主机必须正常运行，或者丢失到存储的数据访问。  
  
**磁盘大小的**，直接附加的存储可以具有 1、 2 或 3 个 Terabyte 磁盘驱动器。 所有数据缩放单位必须都具有相同大小的磁盘。  
  
## <a name="basescaleunit"></a>基础比例单元 
 
基本扩展单元包含最低数量的大脑 power 主机、 数据主机和直连的存储所需的设备。 它包括以下组件。 
  
### <a name="orchestration-host"></a>业务流程主机  
此服务器运行整个系统中枢的 PDW。
  
### <a name="passive-host"></a>被动主机  
此服务器提供高可用性。 它处于联机状态并且准备好运行作业，以防止出现业务流程或数据主机上的故障。 业务流程主机、 被动主机和数据规模单位服务器配置为 Windows 故障转移群集。 每个机架在装置中的需要一个被动主机。  
  
### <a name="optional-passive-host"></a>可选的被动主机  
若要添加更多冗余，您可以选择添加到基本的缩放单位的第二个被动主机。  
  
### <a name="data-scale-unit"></a>数据缩放单位  
基本规模单位都包括一个机架底部放置数据缩放单位。  
  
此图显示了基本扩展单元以及机架和网络。 这是针对分析平台系统设备的最低配置。  
  
![基本的缩放单位](media/base-scale-unit.png "基础比例单元")  
 
