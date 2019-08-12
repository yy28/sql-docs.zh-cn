---
title: 架构比较扩展
titleSuffix: Azure Data Studio
description: 安装和使用 Azure Data Studio 的架构比较扩展（预览版）
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a51d64202d3d906b3106092084628b0a961297ea
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959329"
---
# <a name="schema-compare-extension-preview"></a>架构比较扩展（预览版）
架构比较扩展提供了一种易于使用的体验来比较 .dacpac 文件和数据库，并将所做的更改应用于目标。

此体验目前处于初始预览版。 在[此处](https://github.com/microsoft/azuredatastudio/issues)报告问题和提出功能请求。

## <a name="install-the-schema-compare-extension"></a>安装架构比较扩展

1. 若要打开扩展管理器并访问可用扩展，请选择扩展图标，或在“视图”菜单中选择“扩展”   。
2. 选择某个可用扩展以查看其详细信息。
1. 选择所需的扩展（架构比较）并“安装”它  。

## <a name="how-do-i-start-a-schema-comparison"></a>如何启动架构比较？
* 架构比较的主入口点是右键单击对象资源管理器中的数据库，然后单击“架构比较”  。
* 用户还可以通过搜索”架构比较“来从命令面板启动架构比较对话框 (Ctrl + Shift + P) 

## <a name="why-would-i-use-the-schema-compare"></a>为什么要使用架构比较？
创建架构比较的目的是实现一项功能，即对 .dacpac 文件和数据库中的架构进行比较，并应用更改。

## <a name="next-steps"></a>后续步骤
若要了解有关架构比较的详细信息，[请查看我们的文档。](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions)


