---
title: 源代码管理中 SQL Operations Studio (preview) |Microsoft 文档
description: 了解如何在 SQL Operations Studio (preview) 中配置源代码管理。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f28199262b087ad5362da0ddf56827216aec748
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>使用源代码管理中[!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)]支持的版本/源代码管理的 Git。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>中的 Git 支持[!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)]附带了 Git 源代码控制管理器 (SCM)，但你仍需要[安装 Git (版本 2.0.0 或更高版本)](https://git-scm.com/download)这些功能都可之前。 



## <a name="open-an-existing-git-repository"></a>打开现有的 Git 存储库

1. 下**文件**菜单上，选择**打开文件夹...**
2. 浏览到包含 git，跟踪文件的文件夹，然后单击**选择文件夹**。 本地存储库中的子文件夹是可以在此处选择。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 存储库

1. 选择**源代码管理**，然后选择 git 图标。

   ![源控件 git 图标](media/source-control/source-control.png)

1. 输入你想要初始化所需的 Git 存储库和按下的文件夹的路径**Enter**。

   ![初始化 Git 存储库](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 存储库

[!INCLUDE[name-sos](../includes/name-sos-short.md)]从 VS Code 中，继承其 Git 实现，但当前不支持其他 SCM 提供程序。 有关使用 Git 后打开或初始化存储库的详细信息，请参阅[在 VS Code 中的 Git 支持](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他资源
- [Git 文档](https://git-scm.com/documentation)
