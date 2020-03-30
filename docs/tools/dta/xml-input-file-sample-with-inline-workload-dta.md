---
title: 带有内联工作负载的 XML 输入文件示例
titleSuffix: DTA
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: b12c6f285a7c9eb1e32c33332b00ec624092c3c6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258022"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>内联工作负荷的 XML 输入文件示例 (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

复制以下 XML 输入文件的示例（其中使用 **EventString** 元素指定了一个工作负荷），并将其粘贴到常用的 XML 编辑器或文本编辑器中。 您可以在 XML 输入文件中使用 **EventString** 元素指定一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本工作负荷，而不必使用单独的工作负荷文件。 将此示例复制到编辑工具中后，将为 **服务器**、 **数据库**、 **架构**、 **表**、 **工作负荷**、 **EventString**和 **TuningOptions** 元素指定的值，替换为具体的优化会话所用的值。 有关可以与这些元素一起使用的所有属性和子元素的详细信息，请参阅 [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)。 以下示例只使用了部分可用属性和子元素选项。

## <a name="code"></a>代码

[!code-xml[InputFileSamples#InlineWorkloadInputFile](../../tools/dta/codesnippet/xml/xml-input-file-sample-wi_1.xml)]

## <a name="comments"></a>注释

`USE database_name` EventString **EventString** 语句。

## <a name="see-also"></a>另请参阅

- [启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)
- [查看和使用数据库引擎优化顾问的输出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)
- [XML 输入文件引用（数据库引擎优化顾问）](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)