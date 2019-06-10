---
title: 架构比较扩展
titleSuffix: Azure Data Studio
description: 安装和使用适用于 Azure Data Studio （预览版） 的架构比较扩展
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 15c9b05c418d300b7c65266826df552864d0a5b3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798087"
---
# <a name="schema-compare-extension-preview"></a>架构比较扩展 （预览版）
架构比较扩展提供了一种易于使用的体验来比较.dacpac 文件和数据库，并从源到目标应用所做的更改。

这种体验目前处于其初始预览状态。 报告问题和功能请求[此处。](https://github.com/microsoft/azuredatastudio/issues)

## <a name="install-the-schema-compare-extension"></a>安装架构比较扩展

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 选择要查看其详细信息的可用扩展。
1. 选择所需 （架构比较） 的扩展并**安装**它。

## <a name="how-do-i-start-a-schema-comparison"></a>如何启动架构比较？
* 架构比较的主入口点是右键单击某个数据库在对象资源管理器，并单击**架构比较**。
* 用户还可以通过搜索来启动命令面板 (Ctrl + Shift + P) 的架构比较对话框**架构比较**

## <a name="why-would-i-use-the-schema-compare"></a>为什么要使用架构比较？
架构比较已创建要添加的功能比较从.dacpac 文件和数据库架构，并应用所做的更改。

## <a name="next-steps"></a>后续步骤
若要详细了解架构比较，[检查我们的文档。](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions)


