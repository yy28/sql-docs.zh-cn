---
title: 硬件组件
description: 分析平台系统（AP）使用可缩放的组件，因此你可以根据业务需求购买适当数量的处理和存储。 订购 AP 时，需要结合使用这些核心硬件组件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401144"
---
# <a name="hardware-components-for-analytics-platform-system"></a>用于分析平台系统的硬件组件

分析平台系统（AP）使用可缩放的组件，因此你可以根据业务需求购买适当数量的处理和存储。 订购 AP 时，需要结合使用这些核心硬件组件。 特定硬件供应商可能使用不同的命名约定，或者有其他组件。  
 
  
## <a name="rack-and-network"></a><a name="rackandnetwork"></a>机架和网络 
 
AP 组件都存储在适合你的数据中心的一个或多个机架中。 每个机架附带了配电装置（Pdu）、两个掉电交换机和两个以太网交换机。  
  
![机架和网络](media/rack-and-network.png "AP 和网络")  
  
## <a name="data-scale-unit"></a><a name="datascaleunit"></a>数据缩放单位
 
数据缩放单位包含数据主机和直连存储（DAS）用于处理和存储用户数据。 若要添加容量，请根据硬件供应商支持的配置添加数据缩放单位。 随着数据缩放单位数量的增加，需要根据需要添加其他机架 & 网络组件，以提供更多的电源、网络和机架基础结构。  
  
### <a name="data-host"></a>数据宿主  

数据主机是专用于处理用户数据的服务器。 并行数据仓库（PDW）在每个数据主机上运行一个计算节点。 对于 HPE 设备，数据缩放单位有两个数据主机。 对于 Dell 和量程设备，数据缩放单位有三个数据主机。  
  
### <a name="direct-attached-storage"></a>直接连接的存储
 
直连存储（DAS）是连接到数据主机的磁盘池。 所有数据主机都可以访问任何磁盘。 作为非共享的体系结构的一部分，在数据主机上运行的计算节点不共享单个磁盘。 但是，为了实现高可用性，将共享存储访问权限，并且每个数据主机都可以访问任何磁盘。  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>数据缩放单元体系结构-DELL 和量程
  
![可伸缩性单元](media/scalability-unit-dell.png "Dell 可伸缩性单元")  
  
### <a name="data-scale-unit-architecture---hpe"></a>数据缩放单元体系结构-HPE 
 
![HPE 可伸缩性单元](media/scalability-unit-hpe.png "HPE 可伸缩性单元")  
  
### <a name="data-scale-unit-description"></a>数据缩放单位说明

数据扩展单元具有一个服务器（主机），适用于每个计算节点和一个附加了串行连接 SCSI （SAS）的直接连接的磁盘阵列。 在存储机柜中，磁盘阵列分成两个部分，每个都有冗余的电源。 Windows Server 存储空间通过跨 RAID 1 镜像磁盘对复制数据来管理用户数据。 每个磁盘对中的磁盘存储在不同的磁盘阵列部分。  
  
磁盘阵列还包含热备用磁盘和系统磁盘。 如果磁盘出现故障，存储空间将使用正常运行的磁盘上的数据副本来重建热备用数据的重复副本。 这是一项重要的自我修复功能，可帮助防止数据丢失。  
  
计算节点的磁盘总数：  
  
-   DELL 包含96磁盘 = （3个服务器） * （每个服务器 16 \*个磁盘）（2个磁盘用于冗余磁盘）。  
  
-   HPE 包含64磁盘 = （2个服务器） * （每个服务器 16 \*个磁盘）（冗余磁盘为2个）。  
  
-   此外，每个磁盘阵列都具有热备用磁盘和系统磁盘。  
  
**为实现高可用性**，当计算节点发生故障转移时，它仍然可以通过数据缩放单位中的其他主机来运行和访问其用户数据。 至少一个直接连接的物理主机必须运行，否则对存储的数据访问将丢失。  
  
**对于磁盘大小**，直连存储可以有1个、2个或 3 tb 的磁盘驱动器。 所有数据缩放单位的磁盘大小必须相同。  
  
## <a name="base-scale-unit"></a><a name="basescaleunit"></a>基本缩放单位 
 
基本缩放单位包含设备所需的大脑动力主机、数据主机和直连存储的最小数目。 它包括以下组件。 
  
### <a name="orchestration-host"></a>业务流程主机  
此服务器运行大脑。
  
### <a name="passive-host"></a>被动主机  
此服务器提供高可用性。 它处于联机状态，可以在业务流程或数据主机发生故障时运行作业。 业务流程主机、被动主机和数据缩放单元服务器配置为 Windows 故障转移群集。 设备上的每个机架都需要一个被动主机。  
  
### <a name="optional-passive-host"></a>可选的被动主机  
若要添加更多冗余，可以选择将第二个被动主机添加到基本缩放单位。  
  
### <a name="data-scale-unit"></a>数据缩放单位  
基本缩放单位包含一个位于机架底部的数据缩放单位。  
  
此图显示了基本缩放单位以及机架和网络。 这是分析平台系统设备的最低配置。  
  
![基本缩放单位](media/base-scale-unit.png "基本缩放单位")  
 
