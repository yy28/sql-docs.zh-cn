---
title: “命令”窗口
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 226acc4696b5edacde3b6950c10c8b5370e29b42
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243430"
---
# <a name="transact-sql-debugger---command-window"></a>Transact-SQL 调试器 -“命令”窗口

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用“命令窗口”  可以对“[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 查询编辑器”窗口中当前所调试的代码运行命令，例如调试和编辑命令。 只有在调试模式下才可以使用 **“命令窗口”** 。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器支持许多在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]“命令”  窗口中支持的命令。 有关详细信息，请参阅 [Visual Studio“命令”窗口](https://go.microsoft.com/fwlink/?LinkId=112007)。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>任务列表

**访问“命令”窗口**

- 在 **“调试”** 菜单中，单击 **“启动调试”** 。

**打印变量的值**

- 在“命令窗口”  中，键入 **Debug.Print \<VariableName>** ，然后按 Enter 键。

**列出有关当前线程的信息**

- 在“命令窗口”  中，键入 **Debug.ListThread**，然后按 Enter 键。

**将变量添加到“快速监视”窗口**

- 在“命令窗口”  中，键入 **Debug.QuickWatch \<VariableName>** ，然后按 Enter 键。

## <a name="see-also"></a>另请参阅

[Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)
