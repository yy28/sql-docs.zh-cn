---
title: “命令”窗口 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b6fd133b1a2829d366e09fc340e0b9b7bfb1ff0
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67679560"
---
# <a name="transact-sql-debugger---command-window"></a>Transact-SQL 调试器 -“命令”窗口
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  使用“命令窗口”  可以对“[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 查询编辑器”窗口中当前所调试的代码运行命令，例如调试和编辑命令。 只有在调试模式下才可以使用 **“命令窗口”** 。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器支持许多在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]“命令”  窗口中支持的命令。 有关详细信息，请参阅 [Visual Studio“命令”窗口](https://go.microsoft.com/fwlink/?LinkId=112007)。  
  
## <a name="task-list"></a>任务列表  
 **访问“命令”窗口**  
  
-   在 **“调试”** 菜单中，单击 **“启动调试”** 。  
  
 **打印变量的值**  
  
-   在“命令窗口”  中，键入 **Debug.Print \<VariableName>** ，然后按 Enter 键。  
  
 **列出有关当前线程的信息**  
  
-   在“命令窗口”  中，键入 **Debug.ListThread**，然后按 Enter 键。  
  
 **将变量添加到“快速监视”窗口**  
  
-   在“命令窗口”  中，键入 **Debug.QuickWatch \<VariableName>** ，然后按 Enter 键。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)  
