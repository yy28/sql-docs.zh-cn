---
title: 硬件组件的分析平台系统 |Microsoft 文档
description: 分析平台系统 (AP) 使用可扩展的组件，因此，你可以依据业务需求购买合适的处理和存储量。 当订购 AP 时，你将需要这些核心硬件组件的组合。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9bb7b67a896164fe29611da2091e02c700c46970
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="hardware-components-for-analytics-platform-system"></a>分析平台系统的硬件组件

分析平台系统 (AP) 使用可扩展的组件，因此，你可以依据业务需求购买合适的处理和存储量。 当订购 AP 时，你将需要这些核心硬件组件的组合。 特定硬件供应商可能使用不同的命名约定，或有其他组件。  
 
  
## <a name="rackandnetwork"></a>机架和网络 
 
所有存储在放入你的数据中心的一个或多个机架 AP 组件。 每个机架附带配电装置 (Pdu)、 两个 InfiniBand 交换机和两个以太网交换机。  
  
![机架和网络](media/rack-and-network.png "AP 机架和网络")  
  
## <a name="datascaleunit"></a>数据缩放单位
 
数据扩展单元包含数据主机和直连的存储 (DAS) 来处理和存储用户数据。 若要添加容量你添加根据硬件供应商支持的配置数据缩放单位。 随着数据缩放单位的数量增加，你需要添加其他机架和网络组件，根据需要，提供更大电源、 网络和机架基础结构。  
  
### <a name="data-host"></a>数据主机  

数据主机是专用于处理用户数据的服务器。 并行数据仓库 (PDW) 在每个数据主机上运行一个计算节点。 对于 HPE 设备的数据缩放单位具有数据的两个主机。 Dell 和量程设备中，对于数据缩放单位具有三个数据主机。  
  
### <a name="direct-attached-storage"></a>直连的存储
 
直连的存储 (DAS) 是连接到数据主机的磁盘池。 所有数据主机可以访问的任何磁盘。 无共享的一部分数据主机上运行的计算节点的体系结构，不共享单个磁盘。 但是，以实现高可用性，共享存储访问，并且每个数据主机可以访问的任何磁盘。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>数据缩放单元体系结构-DELL 和量程
  
![可伸缩性单元](media/scalability-unit-dell.png "Dell 可伸缩性单元")  
  
### <a name="data-scale-unit-architecture---hpe"></a>数据缩放单元体系结构-HPE 
 
![HPE 可伸缩性单元](media/scalability-unit-hpe.png "HPE 可伸缩性单元")  
  
### <a name="data-scale-unit-description"></a>数据缩放单元说明

数据缩放单位为每个计算节点和附加与串行连接 SCSI (SAS) 的一个直接附加的磁盘阵列有一个服务器 （主机）。 在 cabinet 的存储中，磁盘阵列分为两部分，每个包含冗余电源。 Windows Server 存储空间管理通过在 RAID 1 镜像磁盘对之间复制数据的用户数据。 每个磁盘对中的磁盘存储在磁盘阵列的不同部分。  
  
磁盘阵列还包含热备用磁盘和系统磁盘。 如果发生磁盘故障，存储空间使用正确的副本的数据磁盘上的正常运行以重新生成上的热备用的数据的副本。 这是重要的自我修复功能，以帮助防止数据丢失。  
  
为计算节点的磁盘的总数：  
  
-   DELL 具有 96 磁盘 = （3 个服务器） * （每个服务器的 16 个磁盘） \* (冗余磁盘为 2 个)。  
  
-   HPE 具有 64 个磁盘 = （2 个服务器） * （每个服务器的 16 个磁盘） \* (冗余磁盘为 2 个)。  
  
-   此外，每个磁盘阵列具有热备用磁盘和系统磁盘。  
  
**为实现高可用性**，当计算节点发生故障转移它可以仍函数和数据缩放单位中的其他主机通过访问其用户数据。 直接连接的物理主机中至少一个必须正常运行，或者丢失到存储的数据访问。  
  
**针对磁盘大小**，直连的存储可以有 1、 2 或 3 Terabyte 磁盘驱动器。 所有数据缩放单位必须都具有相同大小的磁盘。  
  
## <a name="basescaleunit"></a>基本的缩放单位 
 
基本扩展单元包含脑 power 主机、 数据主机和所需的设备直接连接的存储的最小数。 它包括这些组件。  
  
### <a name="orchestration-host"></a>业务流程主机  
此服务器运行 PDW 的大脑。
  
### <a name="passive-host"></a>被动主机  
此服务器提供高可用性。 它处于联机状态并且准备好运行作业，以防还有的业务流程或数据主机上的故障。 业务流程主机、 被动主机和数据扩展单元服务器被配置为 Windows 故障转移群集。 每个机架在设备需要一个被动主机。  
  
### <a name="optional-passive-host"></a>可选的被动主机  
若要添加进一步冗余，你可以选择第二个被动将主机添加到的基本缩放单位。  
  
### <a name="data-scale-unit"></a>数据缩放单位  
基本缩放单位包括一个数据缩放单位其放置在机架的底部。  
  
下图显示的基本缩放单位加上的机架和网络。 这是针对分析平台系统设备的最低配置。  
  
![基本的缩放单位](media/base-scale-unit.png "基本缩放单位")  
 
