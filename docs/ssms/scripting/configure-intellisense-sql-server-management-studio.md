---
title: 配置 IntelliSense (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Options [SQL Server Management Studio], IntelliSense
- modifying IntelliSense options
- IntelliSense [SQL Server], modifying options
ms.assetid: 3ffc9f31-4efa-4c1a-a033-ed1dc48b065f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e148cd3dc64ce93b46a990580be24ace757a87af
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263510"
---
# <a name="configure-intellisense-sql-server-management-studio"></a>配置 IntelliSense (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  默认情况下，大多数 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 选项处于启用状态。 您可以禁用 IntelliSense 选项，转而通过菜单命令或基键组合来调用该选项。  
  
> [!IMPORTANT]  
>  某些更改不会在当前编辑器会话中生效。  必须打开一个新的 Transact-SQL 编辑器会话，才能查看更改。
  
### <a name="to-turn-statement-completion-options-off-by-default"></a>默认关闭语句结束选项  

> [!NOTE]
> SQL 数据仓库不支持 IntelliSense。
>
>
  
1.  在“工具”  菜单上，单击“选项”  。  
  
2.  展开“文本编辑器”  ，展开“所有语言”  、“Transact-SQL”  或“XML”  ，然后单击“常规”  。  
  
3.  清除不想使用的“语句结束”选项的复选框，然后单击 **“确定”** 。  
  
### <a name="to-modify-transact-sql-intellisense-options"></a>修改 Transact-SQL IntelliSense 选项  
  
1.  在“工具”  菜单上，单击“选项”  。  
  
2.  展开“文本编辑器”  ，展开“Transact-SQL”  ，然后单击“IntelliSense”  。  
  
3.  清除不需要的 IntelliSense 选项的复选框。  
  
4.  若要更改禁用 IntelliSense 功能时的脚本大小，请从 **“最大脚本大小”** 列表中选择大小。  
  
5.  若要更改完成列表中的函数名称应用的大小写，请从“内置函数名称的大小写”  列表中选择大小写规范。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
