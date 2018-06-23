---
title: 启用禁用写回对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0455e8f9efc76fa8ab254ac89d17b5ffb180e4ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129987"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>启用禁用写回对话框 (Analysis Services-多维数据)
  可以使用“启用/禁用写回”对话框，为多维数据集中的度量值组启用或禁用写回。 对度量值组启用写回将定义一个写回分区，并为该度量值组创建一个写回表。 对度量值组禁用写回将删除写回分区（但不会删除写回表），以免发生意外数据丢失。 通过执行以下操作可以显示“启用/禁用写回”对话框：  
  
-   在多维数据集设计器中的“分区”选项卡上，单击“度量值组”窗格中的“写回设置”。  
  
-   在多维数据集设计器中的“分区”选项卡上，在“度量值组”窗格的“分区”网格中右键单击某个分区，然后从上下文菜单中选择“写回设置”。  
  
## <a name="options"></a>“常规”  
 **表名**  
 键入要为所选分区创建的写回表的名称。 写回表存储对来自客户端应用程序的度量值组所做的更改。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
 **数据源**  
 选择包含写回表的数据源。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
 **新建**  
 单击显示“连接管理器”对话框，并定义新数据源以包含写回表。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
  