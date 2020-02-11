---
title: 从 IHV 获取信息
description: 要从 IHV 获取的有关分析平台系统设备的信息。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 730cf09ab7e45ea74070db591592fdb871243a77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401058"
---
# <a name="information-to-obtain-from-your-ihv"></a>要从 IHV 获取的信息
当你的独立硬件供应商（IHV）将新的 SQL Server PDW 设备交付给你时，他们还将提供有关设备硬件和设备上所执行的配置的信息。 你将需要此信息来管理你的设备。  
  
以下列表显示了你的 IHV 中通常需要的信息。 在某些情况下，需要其他信息或其他信息。 请与你的 IHV 联系，确保已通过设备交付将所有相关信息转让给你。  
  
|||  
|-|-|  
|**信息或文档**|**说明**|  
|物料清单（BOM）|物料清单列出了设备中包含的组件。 此信息是确认所有组件均已传递所必需的。<br /><br />**重要提示：** 物料清单应该包含每个设备节点和每个完整机架的重量。 规划如何处理和移动设备组件以及确保你的数据中心可以容纳该设备时，此信息非常重要。 如果你的 BOM 不包含节点权重，请确保从你的 IHV 为所有节点获取此信息。|  
|布线图|布线图显示了如何连接每个设备机架的网络、电源和其他电缆。 在数据中心中安装设备时，以及在需要删除或更换组件时，需要使用这些关系图。|  
|设备搭架要求|在你的设备可以安装到你的数据中心之前，你需要了解你的数据中心是否满足设备的气流和电缆长度要求，以及组件的大小和电源要求。 有关设备组件权重（也是必需的）的信息，请参阅上面的物料清单（BOM）。|  
  
