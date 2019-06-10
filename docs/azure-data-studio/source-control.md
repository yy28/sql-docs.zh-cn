---
title: 源代码管理
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中配置源代码管理
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6431b869af8abc91a9de319f32c0576b82428a0a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798029"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 使用原始碼控制

[!INCLUDE[name-sos](../includes/name-sos-short.md)]支援 Git 版本/原始碼控制。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的 Git 支援

[!INCLUDE[name-sos](../includes/name-sos-short.md)]內附 Git 原始碼控制管理員 (SCM)，但是在使用功能之前，您仍然需要[安裝 Git (2.0.0 版或更新版本)](https://git-scm.com/download)。 



## <a name="open-an-existing-git-repository"></a>開啟現有的 Git 儲存庫

1. 在**檔案**功能表下，選取**開啟資料夾...**
2. 瀏覽至包含 git 追蹤檔案的資料夾，然後按一下 **選取資料夾**。 在這裡可以選取本機儲存庫的子資料夾。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 存储库

1. 选择**源代码管理**，然后选择 git 图标。

   ![源控件的 git 图标](media/source-control/source-control.png)

1. 輸入您想要初始化為 Git 儲存庫的資料夾路徑然後按下**Enter**。

   ![初始化 Git 存储库](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 儲存庫

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會從 VS Code 繼承其 Git 實作，但目前不支援其他 SCM 提供者。 在您開啟或初始化儲存庫之後，如需使用 Git 的詳細資訊，請參閱 [VS Code 中的 Git 支援](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他资源
- [Git 文档](https://git-scm.com/documentation)
