---
title: 如何参与编辑 SQL Server 文档 | Microsoft Docs
ms.date: 03/19/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1885c57cfcf21dcdb877fc4c59b229636b74c137
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>如何参与编辑 SQL Server 文档

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

任何人都可以参与编辑 SQL Server 文档。 这包括更正拼写错误、提出更好的解释以及改进技术的准确性。 本文介绍如何开始参与内容编辑以及此过程的工作原理。

可通过以下两个主要工作流参与编辑：

|||
|---|---|
| [在浏览器中编辑](#githubui) | 适用于对任何文章进行少量快速编辑。 |
| [使用工具在本地编辑](#tools) | 适用于更复杂的编辑、涉及多篇文章的编辑，以及针对 docs.microsoft.com 的频繁编辑。 |

## <a id="githubui"></a>在浏览器中编辑

以下步骤提供了在浏览器中对 SQL Server 内容进行简单编辑的概述。 [次要更改或间歇更改的 GitHub 参与工作流](https://docs.microsoft.com/contribute/contribute/light-workflow)一文记录了完整过程。

1. 包括本文在内的每篇文章右侧均有一个“编辑”按钮。 查找要更改的文章，然后单击“编辑”按钮开始编辑。

   ![SQL 文章的“编辑”按钮](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   docs.microsoft.com 上的所有内容托管在各个 GitHub 存储库中。 单击编辑按钮时，将转到 sql-docs 存储库中的文章。 或者，若要编辑 Azure 文档中的 SQL 文章，则将转到 azure-docs 存储库。 

1. 接着，单击 GitHub 中文章右上角的铅笔图标。

   ![编辑按钮](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > 必须登录到 GitHub 才能编辑文章。 如果没有 GitHub 帐户，请参阅 [GitHub 帐户设置](https://docs.microsoft.com/contribute/contribute/get-started-setup-github)。 创建新帐户后，还必须通过 GitHub 验证电子邮件地址，然后才能开始编辑。

1. 在浏览器中编辑文章。 所有文章都是以 Markdown 编写的。 如需 Markdown 相关帮助，可以查看 [Markdown 基本信息](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)。 还可以通过观察发布的文章如何呈现现有 Markdown 进行了解。

1. 向下滚动到编辑窗口底部，输入更改的标题，然后单击“建议文件更改”按钮。

   ![建议拉取请求](./media/sql-server-docs-contribute/propose-file-change.png)

1. 在下一页上，单击“创建拉取请求”。

   ![创建拉取请求](./media/sql-server-docs-contribute/create-pull-request.png)

1. 输入拉取请求的标题和说明。 然后再次单击“创建拉取请求”。

   ![创建拉取请求](./media/sql-server-docs-contribute/create-pull-request2.png)

此时，系统应指导你在拉取请求的注释中完成此过程的剩余部分。 [参与者指南](https://docs.microsoft.com/contribute/contribute/light-workflow)中提供了完整过程和其他详细信息。

## <a id="tools"></a>使用工具在本地编辑

另一个编辑选项是创建 sql-docs 或 azure-docs 存储库的分支并将其克隆到本地计算机。 然后可以使用 Markdown 编辑器和 git 客户端提交所做的更改。 此工作流适用于更复杂或涉及多个文件的编辑。 另外，它也适用于针对 docs.microsoft.com 的频繁参与者。

若要使用此方法参与编辑，请参阅以下文章：

- [创建 GitHub 帐户](https://docs.microsoft.com/contribute/contribute/get-started-setup-github)
- [安装内容创作工具](https://docs.microsoft.com/contribute/contribute/get-started-setup-tools)
- [设置本地 Git 存储库](https://docs.microsoft.com/contribute/contribute/get-started-setup-local)
- [使用工具参与编辑](https://docs.microsoft.com/contribute/contribute/full-workflow)

如果提交包含对文档的重大更改的拉取请求，则将在 GitHub 中收到一条注释，要求提交联机“贡献许可协议 (CLA)”。 必须先完成联机窗体，然后系统才会接受你的拉取请求。

## <a name="recognition"></a>识别

如果接受了你所做的更改，则系统会在文章顶部将你识别为参与者。

![内容编辑识别](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>sql-docs 概述

本部分提供一些有关在 sql-docs 存储库中工作的其他指导。

> [!IMPORTANT]
> 本部分中的信息特定于 sql-docs。若要编辑 Azure 文档中的 SQL 文章，请参阅 [GitHub 上 azure-docs 存储库的自述文件](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md)。

[sql-docs](https://github.com/MicrosoftDocs/sql-docs) 存储库使用多个标准文件夹来组织内容。

| 文件夹 | Description |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | 包含所有已发布的 SQL Server 内容。 子文件夹有逻辑地组织内容的不同区域。 |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | 包括包含文件。 这些文件是可以包含在一个或多个其他主题中的内容块。 |
| **./media** | 每个文件夹可以有一个用于文章图像的“媒体”子文件夹。 “媒体”文件夹又包含名称与图像出现的主题名称相同的子文件夹。 图像应为字母全部小写且没有空格的 .png 文件。 |
| **TOC.MD** | 目录文件。 每个子文件夹都可选择使用 TOC.MD 文件。 |

#### <a name="applies-to-includes"></a>“适用范围”包含

每篇 SQL Server 文章的标题后都包含“适用范围”包含文件。 这表示文章适用于哪些 SQL Server 区域或版本。

请查看以下从 appliesto-ss-asdb-asdw-pdw-md.md 包含文件中拉取的 Markdown 示例。

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

这将在文章顶部添加以下文本：

![“适用范围”文本](./media/sql-server-docs-contribute/applies-to.png)

若要查找文章的正确适用范围包含，请使用以下提示：

- 查看包含相同功能或相关任务的其他文章。 如果编辑此文章，则可针对适用范围包含链接复制 Markdown（可取消编辑而不提交编辑）。
- 针对包含文本“适用范围”的文件搜索 [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) 目录。 可使用 github 中的“查找”按钮快速筛选。 单击文件，查看其呈现方式。
- 注意命名约定。 如果名称中包含 x，它们通常是占位符，表示缺少对服务的支持。 例如，appliesto-xx-xxxx-asdw-xxx-md.md 表示仅支持 Azure SQL 数据仓库，因为仅拼写出了 asdw，而其他字段具有 x。
- 某些包含指定了版本号，如 tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md。 仅当知道通过特定版本的 SQL Server 引入了此功能时才使用这些包含。 

## <a name="contributor-resources"></a>参与者资源

- [docs.microsoft.com 参与者指南](https://docs.microsoft.com/en-us/contribute/)
- [Microsoft 风格指南](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Markdown 基本信息](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> 如果有产品反馈而不是文档反馈，[请在此处提供有关 SQL Server 产品的反馈](https://feedback.azure.com/forums/908035-sql-server)。

## <a name="next-steps"></a>后续步骤

浏览 GitHub 上的 [sql-docs 存储库](https://github.com/MicrosoftDocs/sql-docs)。

查找文章，提交更改，并帮助 SQL Server 社区。 

谢谢！


