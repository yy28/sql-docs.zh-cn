---
title: 定义赋值和其他脚本命令 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: caa3b6f49ce778b78f066abf687a3a51b61cc487
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075819"
---
# <a name="define-assignments-and-other-script-commands"></a>定义赋值和其他脚本命令
  在多维数据集设计器的“计算”选项卡上，单击工具栏中的“新建脚本命令”图标以创建空脚本。 创建新脚本时，该脚本最初以空白标题显示在“计算”选项卡的 **“脚本组织程序”** 窗格中。您在“计算表达式”窗格中键入的字符将在 **“脚本组织程序”** 中显示为项的名称。 因此，您可能要在第一行中键入被注释的名称，以更方便地标识 **“脚本组织程序”** 窗格中的脚本。 有关详细信息，请参阅 [对 Microsoft SQL Server 2005 中的 MDX 脚本编写的介绍](https://go.microsoft.com/fwlink/?LinkId=81892)。 有关与 MDX 查询和计算相关的性能问题的详细信息，请参阅"编写有效的 MDX"一节中[SQL Server 2005 Analysis Services 性能指南](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)。  
  
> [!IMPORTANT]  
>  当您最初切换到多维数据集设计器的 **“计算”** 选项卡时， **“脚本组织程序”** 窗格将包含具有 CALCULATE 命令的单个脚本。 CALCULATE 命令控制多维数据集中单元的聚合，仅当您要手动指定多维数据集的聚合方式时，才应编辑该命令。  
  
 可以使用“计算表达式”窗格以多维表达式 (MDX) 语法生成表达式。 生成表达式时，可以将多维数据集组件、函数和模板从 **“计算工具”** 窗格拖动或复制到“计算表达式”窗格。 这种做法可以将项的脚本添加到“计算表达式”窗格中您放置或粘贴的位置。 用适当的值替换参数及其分隔符（« 和 »）。  
  
> [!IMPORTANT]  
>  当使用“计算表达式”窗格编写包含多个语句的表达式时，请确保 MDX 脚本中除最后一行外的所有行都以分号 (;) 结尾。 将计算串联为单个 MDX 脚本并且每个脚本后都追加一个分号，以确保 MDX 脚本可以正确编译。 如果您在“计算表达式”窗格中为脚本的最后一行添加分号，多维数据集将会正确生成和部署，但不能对其运行查询。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的计算](calculations-in-multidimensional-models.md)  
  
  
