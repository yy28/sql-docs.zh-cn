---
title: "Azure HDInsight 连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
caps.latest.revision: 4
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 080cd1184d3c29673ac476d6fe6087b697160544
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 连接管理器
**Azure HDInsight 连接管理器**使 SSIS 包能够连接到 Azure HDInsight 群集。

**Azure HDInsight 连接管理器**的组成部分[用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

若要创建和配置**Azure HDInsight 连接管理器**，按照以下步骤：

1. 在**添加 SSIS 连接管理器**对话框中，选择**AzureHDInsight**，然后单击**添加**。
2. 在**Azure HDInsight 连接管理器编辑器**对话框框中，指定**群集 DNS 名称**（不带协议前缀），**用户名**，和**密码**连接到 HDInsight 群集。
3. 单击 **“确定”** 关闭对话框。
4. 你可以看到你在“属性”  窗口中创建的连接管理器的属性。

