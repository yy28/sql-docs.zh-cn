---
title: "\"启用-禁用写回\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
ms.openlocfilehash: ac29fc0d1539ae75ca5f54ad48f1779692b9a6df
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528405"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>"启用-禁用写回" 对话框（Analysis Services 多维数据）
  可以使用“启用/禁用写回”**** 对话框，为多维数据集中的度量值组启用或禁用写回。 对度量值组启用写回将定义一个写回分区，并为该度量值组创建一个写回表。 对度量值组禁用写回将删除写回分区（但不会删除写回表），以免发生意外数据丢失。 通过执行以下操作可以显示“启用/禁用写回”**** 对话框：  
  
-   在多维数据集设计器中的“分区”**** 选项卡上，单击“度量值组”**** 窗格中的“写回设置”****。  
  
-   在多维数据集设计器中的“分区”**** 选项卡上，在“度量值组”**** 窗格的“分区”**** 网格中右键单击某个分区，然后从上下文菜单中选择“写回设置”****。  
  
## <a name="options"></a>选项  
 **表名**  
 键入要为所选分区创建的写回表的名称。 写回表存储对来自客户端应用程序的度量值组所做的更改。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
 **数据源**  
 选择包含写回表的数据源。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
 **新建**  
 单击显示“连接管理器”**** 对话框，并定义新数据源以包含写回表。  
  
> [!NOTE]  
>  如果未启用写回，将禁用此选项。  
  
  
