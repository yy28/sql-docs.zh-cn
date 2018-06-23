---
title: Azure HDInsight 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPHDICM.F1
- SQL11.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 850a978d-5dba-45b6-a10e-306aafbc353d
caps.latest.revision: 2
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 3d9486108e7f16870d2bf4e22f05b8a0a288b664
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027297"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 连接管理器
Azure HDInsight 连接管理器可实现 SSIS 包与 Azure HDInsight 群集的连接。

若要创建和配置 Azure HDInsight 连接管理器，请执行以下步骤：

1. 在“添加 SSIS 连接管理器” 对话框中，选择“AzureHDInsight”，然后单击“添加” 。
2. 在“Azure HDInsight 连接管理器编辑器”对话框中，为要连接到的 HDInsight 群集指定群集 DNS 名称（不带协议前缀）、用户名和密码。
3. 单击 **“确定”** 关闭对话框。
4. 你可以看到你在“属性”  窗口中创建的连接管理器的属性。