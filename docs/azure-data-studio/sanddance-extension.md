---
title: 有关 Azure 数据 Studio sandDance
titleSuffix: Azure Data Studio
description: 如何在 Azure Data Studio 中使用 SandDance
ms.custom: seodec18
ms.date: 04/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: dd63f490ed1c635abfb6bef6972363cfba3c96bc
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59981231"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance 的 Azure 数据 Studio （预览版）
Azure Data Studio 现在提供了一种方法来创建您正在从事的.csv 和.tsv 文件的快速可视化效果。 这包括在你的 SQL Server 2019 大数据群集中的本地文件或 HDFS 上的文件。 如果想要具有快速查看数据，并了解这怎么回事，此扩展插件十分有用。 我们使用从 Microsoft Research，可以生成数据的就地可视化效果称为 SandDance 的技术。

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

通过使用易于理解的视图，SandDance 可帮助你找到有关你的数据，其中讲述故事支持的数据，打开帮助中构建基于证据的情况下，测试假设，深入到图面上的说明，支持决策进行购买，或关联到更广泛、 现实世界的上下文数据。

SandDance 使用单元可视化效果，在屏幕应用您的数据库中的行和标记之间的一对一映射。
视图之间的平滑动画的转换帮助您维护上下文，如与数据交互。

## <a name="usage"></a>用法

右键单击本地.csv 或.tsv 文件，然后选择*视图中 SandDance*。

如果您连接到 SQL Server 2019 大数据群集并选择在 HDFS 中的.csv 或.tsv 文件上右键单击*视图中 SandDance*。

## <a name="known-issues"></a>已知问题

当前你的数据应具有唯一标识符的第一列。

现在我们不会制定可视化的行计数。 但是，内存使用量超过按比例到数量的行，因此，我们建议的数据集或视图仅限于大约 100 万行。

请参阅[已知问题](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>发行说明

### <a name="100"></a>1.0.0

Azdata sanddance 的初始版本

## <a name="next-steps"></a>后续步骤
若要了解详细信息，[请访问 GitHub 存储库。](https://github.com/Microsoft/SandDance)