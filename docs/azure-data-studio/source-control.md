---
title: 源代码管理
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中配置源代码管理
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c278bcf6cff451396b3d677b203f207b68fd6dc5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959280"
---
#  <a name="using-source-control-in-name-sos"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 中使用源代码管理

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 支持用于版本/源代码管理的 Git。


## <a name="git-support-in-name-sos"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中的 Git 支持

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 附带 Git 源控制管理器 (SCM)，但仍需要[安装 Git（版本 2.0.0 或更高版本）](https://git-scm.com/download)，然后才能使用这些功能。 



## <a name="open-an-existing-git-repository"></a>打开现有 Git 存储库

1. 在“文件”菜单下，选择“打开文件夹...”  
2. 浏览到包含 Git 所跟踪文件的文件夹，然后单击“选择文件夹”  。 可在此处选择本地存储库中的子文件夹。


## <a name="initialize-a-new-git-repository"></a>初始化新 Git 存储库

1. 选择“源代码管理”，然后选择 Git 图标  。

   ![源代码管理 Git 图标](media/source-control/source-control.png)

1. 输入指向要初始化为 Git 存储库的文件夹的路径，然后按 Enter  。

   ![初始化 Git 存储库](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 存储库

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 从 VS Code 继承其 Git 实现，但目前不支持其他 SCM 提供程序。 有关在打开或初始化存储库后使用 Git 的详细信息，请参阅 [VS Code 中的 Git 支持](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他资源
- [Git 文档](https://git-scm.com/documentation)
