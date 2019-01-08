---
title: 如何编辑 CDC 实例属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2d15f17b867cd02d700ce6c749edddaa2c65083
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772939"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>如何编辑 CDC 实例属性
  本过程介绍如何使用 CDC 设计器控制台编辑 CDC 实例的配置属性。  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>编辑 CDC 实例的配置属性  
  
1.  从 **“开始”** 菜单上，选择 **“CDC 设计器控制台”**。  
  
2.  在左侧的窗格中，展开 **“变更数据捕获”** ，然后展开包含您要编辑其属性的实例的服务。  
  
3.  选择要编辑其属性的实例的名称。  
  
4.  从 CDC 设计器控制台右侧的“操作”窗格中，单击 **“属性”**。  
  
     也可以右键单击要编辑其属性的实例，然后单击“属性”。  
  
5.  在属性编辑器中，在以下选项卡中编辑属性：  
  
    -   **Oracle**:使用**Oracle**在属性编辑器中对在新建实例向导创建 CDC 数据库页中提供的说明进行更改以及对 Oracle 日志挖掘数据库连接信息进行更改的选项卡。  
  
         有关可在此选项卡中编辑的内容的信息，请参阅 [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md)。  
  
    -   **表**:使用 **“表”** 选项卡可对您从 Oracle 源数据库中选择的表和列进行更改。  
  
         有关可在此选项卡中编辑的内容的信息，请参阅 [Edit Tables](edit-tables.md)。  
  
    -   **脚本**:使用**脚本**选项卡以运行或重新运行脚本将设置补充日志记录对 Oracle 源数据库。  
  
         有关可在此选项卡中执行的操作的信息，请参阅 [Review and Generate Supplemental Logging Scripts](review-and-generate-supplemental-logging-scripts.md)。  
  
    -   **高级**：使用 **“高级”** 选项卡可以向 CDC 实例添加特殊属性。  
  
         有关可在此选项卡中执行的操作的信息，请参阅 [Edit the Advanced Properties](edit-the-advanced-properties.md)。  
  
  
