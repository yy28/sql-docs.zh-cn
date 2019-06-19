---
title: 如何查看 CDC 实例属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bce9b82-7bbd-41df-b3f4-4b40b8bad474
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0fddc9de23354536b7e6ed1956ad903ce559184
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728708"
---
# <a name="how-to-view-the-cdc-instance-properties"></a>如何查看 CDC 实例属性

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  本过程介绍如何使用 CDC 设计器控制台查看与您创建的实例有关的信息，以便帮助管理实例操作。  
  
### <a name="to-view-information-about-a-specific-instance"></a>查看有关特定实例的信息  
  
1.  从 **“开始”** 菜单上，选择 **“CDC 设计器控制台”** 。  
  
2.  在左侧的窗格中，展开 **“变更数据捕获”** ，然后展开包含您要查看的实例的服务。  
  
3.  选择要使用的实例的名称。  
  
     与该实例有关的信息将显示在 CDC 设计器控制台的中央部分。 它分为四个选项卡。 所有选项卡均为只读。  
  
     **“状态”**  
     此选项卡显示有关该实例的变更数据捕获的当前状态的信息。 有关此选项卡中显示的内容的信息，请参阅 **Manage a CDC Instance** 中的 [“查看器选项卡”](../../integration-services/change-data-capture/manage-a-cdc-instance.md)部分。  
  
     **Oracle**  
     此选项卡显示与 CDC 实例和 Oracle 源数据库有关的一般信息。 有关此选项卡中显示的内容的信息，请参阅 [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)。  
  
     **表**  
     此选项卡显示有关变更数据捕获中包含的表的信息。 它还列出捕获的列。 有关此选项卡中显示的内容的信息，请参阅 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)。  
  
     **高级**  
     此选项卡显示在属性编辑器中定义的高级属性的列表。 有关此选项卡中显示的内容的信息，请参阅 [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)。  
  
  
