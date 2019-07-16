---
title: 从 IHV-分析平台系统中获取信息 |Microsoft Docs
description: 若要从有关分析平台系统 appliance IHV 中获取的信息。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 016a20567968e45456be79c8c67e77d7c3fbb2bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960837"
---
# <a name="information-to-obtain-from-your-ihv"></a>若要从 IHV 中获取的信息
当独立硬件供应商 (IHV) 为您提供新的 SQL Server PDW 设备时，它们还将提供它们在你的设备上执行的设备硬件和配置信息。 你将需要此信息来管理你的设备。  
  
以下列表显示了从 IHV 通常所需的信息。 在某些情况下，需要额外使用或其他信息。 请与 IHV 以确保已使用设备交付转让给你的所有相关信息。  
  
|||  
|-|-|  
|**信息或文档**|**说明**|  
|物料清单 (BOM)|在材料清单列出了你的设备中包含的组件。 此信息才可确认所有组件已都发送。<br /><br />**重要提示：** 在材料清单应包含权重为每个设备节点和每个完整的机架。 规划如何处理和移动设备组件时，此信息非常重要，并确保你的数据中心可以容纳多设备。 如果你物料清单不包含节点权重，请确保从所有节点 IHV 中获取此信息。|  
|缆线关系图|缆线连接关系图显示如何连接网络、 电源和每个设备的其他电缆机架。 在数据中心中，安装该设备时需要这些关系图，任何时候您需要删除或更换的组件。|  
|设备严苛的需求|你的设备可以安装在你的数据中心之前，需要知道的气流和电缆长度要求的设备，以及大小和组件的电源要求是否满足你的数据中心。 另请参阅物料清单 (BOM) 上面有关设备组件权重，这也是必需。|  
  
