---
title: 连接到报表或数据馈送 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connreportdatafeed.f1
ms.assetid: e0ccfb0b-e646-4de8-b7da-f88c986c96e4
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 726007e635a41295c682ebc929e909fda8f0b0a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210287"
---
# <a name="connect-to-a-report-or-data-feed-ssas"></a>连接到报表或数据馈送 (SSAS)
  **“表导入向导”** 的这一页可用于连接到数据馈送。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
## <a name="from-a-report"></a>从报表  
 **友好连接名称**  
 键入数据馈送连接的友好名称。  
  
 **报表路径**  
 列出生成数据馈送的 SQL Server Reporting Services 报表的 URL。 单击 **“浏览”** 可以指定报表的 URL。  
  
 单击 **“查看报表”** 可以显示报表。  
  
 **“浏览”**  
 导航至报表所在的位置。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
## <a name="from-an-azure-datamarket-dataset"></a>从 Azure DataMarket 数据集  
 **友好连接名称**  
 键入数据馈送连接的友好名称。  
  
 **数据馈送的 URL**  
 键入 Atom 服务文档（.atomsvc、.atom）的完整路径或者键入单个数据馈送的 URL，或者单击“浏览”以便选择某一 Atom 服务文档。  
  
 **“浏览”**  
 导航至报表所在的位置。  
  
 单击 **“查看可用的 Azure DataMarket 数据集”** 可显示可用数据集。  
  
 **帐户密钥**  
 指定用于访问 Microsoft Azure 市场数据集订阅的帐户密钥。  
  
 **查找**  
 查找与 Windows Live 帐户关联的帐户密钥。  
  
 **保存我的帐户密钥**  
 使用数据连接保存帐户密钥（已加密）。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
## <a name="from-other-feeds"></a>从其他馈送  
 **友好连接名称**  
 键入数据馈送连接的友好名称。  
  
 **数据馈送的 URL**  
 键入 Atom 服务文档（.atomsvc、.atom）的完整路径或者键入单个数据馈送的 URL，或者单击“浏览”以便选择某一 Atom 服务文档。  
  
 单击 **“包括所有馈送列”** 可以指定是否导入所有数据馈送列。  
  
 **“浏览”**  
 导航至数据馈送所在的位置。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  
