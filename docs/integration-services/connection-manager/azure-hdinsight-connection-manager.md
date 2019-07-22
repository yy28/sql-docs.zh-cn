---
title: Azure HDInsight 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: c57abdf2cd6fbdf5cbb0953f1604440d714e1e7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968250"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 连接管理器

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Azure HDInsight 连接管理器可实现 SSIS 包与 Azure HDInsight 群集的连接。

Azure HDInsight 连接管理器是[适用 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组件。

若要创建和配置 Azure HDInsight 连接管理器，请执行以下步骤：

1. 在“添加 SSIS 连接管理器” 对话框中，选择“AzureHDInsight”，然后单击“添加” 。
2. 在“Azure HDInsight 连接管理器编辑器”对话框中，为要连接到的 HDInsight 群集指定群集 DNS 名称（不带协议前缀）、用户名和密码。
3. 单击 **“确定”** 关闭对话框。
4. 你可以看到你在“属性”  窗口中创建的连接管理器的属性。
