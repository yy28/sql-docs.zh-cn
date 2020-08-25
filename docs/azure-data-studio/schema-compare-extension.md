---
title: 架构比较扩展
description: 了解如何安装和使用 Azure Data Studio 架构比较扩展，以便轻松比较两个数据库，并选择性地更改其中一个数据库，使其与另一个数据库匹配。
ms.custom: seodec18
ms.date: 11/04/2019
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 928c258dff70f861c33cc59125171a467eb12bf8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766216"
---
# <a name="schema-compare-extension"></a>架构比较扩展
架构比较扩展提供了一种易于使用的体验，以比较两个数据库定义，并将源的区别应用于目标。


## <a name="features"></a>功能

* 比较两个 dacpac 文件或数据库的架构
* 将结果视为一组要匹配源则必须针对目标执行的操作
* 选择性地排除结果中列出的操作
* 设置控制比较范围的选项
* 将更改应用到目标，或生成具有相同效果的脚本
* 保存比较

![架构比较：示例比较](media/extensions/schema-compare-extension/schema-compare.png)


## <a name="why-would-i-use-the-schema-compare-extension"></a>为什么要使用架构比较扩展？

手动管理和同步不同的数据库版本可能比较繁琐。 架构比较扩展可以简化数据库比较过程，并在同步数据库时提供完全控制 &mdash; 可以在应用更改之前有选择地筛选特定差异和类别。 架构比较扩展是一个可节省时间和代码的可靠工具。

![架构比较：“选项”对话框](media/extensions/schema-compare-extension/schema-compare-options.png)


## <a name="install-the-extension"></a>安装扩展

1. 选择“扩展”图标以查看可用扩展。

    ![扩展管理器图标](media/extensions/extension-manager-icon.png)

2. 搜索“架构比较”扩展并选择它以查看其详细信息  。 单击“安装”，以添加扩展  。

3. 安装后，重载以启用 Azure Data Studio 中的扩展（仅在第一次安装扩展时需要进行此操作）  。


## <a name="launch-a-schema-compare"></a>启动“架构比较”

1. 要打开“架构比较”对话框，右键单击对象资源管理器中的数据库，然后单击“架构比较”   。 你选择的数据库将设置为要比较的源数据库。

    ![“架构比较”启动菜单](media/extensions/schema-compare-extension/schema-compare-launch.png)


2. 选择其中一个省略号 (...)，更改“架构比较”的源数据库和目标数据库，然后单击“确定”。

    ![schema compare select source/target](media/extensions/schema-compare-extension/schema-compare-select-source-target.png)

3. 要自定义比较，请在工具栏中单击“选项”按钮  。

4. 单击“比较”以查看比较结果  。


## <a name="next-steps"></a>后续步骤

若要了解有关架构比较的详细信息，[请查看我们的文档。](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)
在[此处](https://github.com/microsoft/azuredatastudio/issues)报告问题和提出功能请求。