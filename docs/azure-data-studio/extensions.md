---
title: 添加扩展
titleSuffix: Azure Data Studio
description: 将扩展市场中的扩展添加到 Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 10/03/2019
ms.openlocfilehash: 6f0a2ab021873a2a9414bfbcdb7aed63c2d31056
ms.sourcegitcommit: cf268c4e39edf00a8552466e9440e79e6a5d0084
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2019
ms.locfileid: "72166713"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>扩展 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 功能

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中的扩展提供向基本 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 安装添加更多功能的简便方法。 

扩展由 Azure Data Studio 团队 (Microsoft) 以及第三方社区（你）提供。 有关创建扩展的详细信息，请参阅[扩展创作](extension-authoring.md)。


## <a name="add-azure-data-studio-extensions"></a>添加 Azure Data Studio 扩展

1. 通过选择扩展图标或选择“视图”菜单中的“扩展”来访问可用扩展。

    ![扩展管理器图标](media/extensions/extension-manager-icon.png)

    还可通过按 `Ctrl+Shift+X` (Windows/Linux) 或 `Command+Shift+X` (Mac) 来快速访问扩展管理器。

2. 选择某个可用扩展以查看其详细信息。
    ![扩展详细信息](media/extensions/extension-details.png)

3. 选择所需的扩展并“安装”它。

4. 安装后，重载以启用 Azure Data Studio 中的扩展（仅在第一次安装扩展时需要进行此操作）。

如果访问 Azure Data Studio 上的扩展管理器时遇到问题，则可以在 [GitHub Wiki](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions) 上下载所需的扩展。


## <a name="access-installed-azure-data-studio-extensions"></a>访问已安装的 Azure Data Studio 扩展

每个扩展都以不同的方式增强你在 Azure Data Studio 中的体验。 因此，扩展的入口点可能会有所不同。 请参阅已安装的扩展的单独文档，了解关于如何在安装该扩展后访问其功能的信息。
