---
title: 第3课：使用 dta 命令提示实用工具 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2881a2a118306f9d567236516f05bb29ad2d60a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "68186573"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>第 3 课：使用 dta 命令提示实用工具
  **dta** 命令提示实用工具除了包含数据库引擎优化顾问提供的功能之外，还包含其他功能。  
  
 通过数据库引擎优化顾问 XML 架构，您可以使用自己喜爱的 XML 工具创建实用工具的输入文件。 该架构随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起安装，可在 C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd 中找到。  
  
 数据库引擎优化顾问 XML 架构也可通过 [此 Microsoft 网站](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)在线获得。  
  
 数据库引擎优化顾问 XML 架构在设置优化选项时可提供更大的灵活性。 例如，可通过它执行“假设分析”。 “假设分析”包括：为要优化的数据库指定一组现有的假设物理设计结构，然后使用数据库引擎优化顾问对该数据库进行分析，以判定此假设物理设计是否能改善查询处理性能。 此类分析具有的优点是，在评估新配置时不会引起实际实施它的开销。 如果假设物理设计不能提供预期的性能改善，则可以方便地进行更改和重新分析，直到获得能够满足需要的配置为止。  
  
 此外，通过结合使用数据库引擎优化顾问 XML 架构和 **dta** 命令提示实用工具，可以将数据库引擎优化顾问功能加入到脚本中，并可将其与其他数据库设计工具一起使用。  
  
 使用数据库引擎优化顾问的 XML 输入功能不在本课程的讨论范围之内。  
  
 本课程介绍了 **dta** 命令提示实用工具的基本语法，如何访问帮助，以及如何优化简单的工作负荷。  
  
 本节包含以下主题：  
  
-   启动**dta**命令提示实用工具并优化工作负荷  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [启动 dta 命令提示实用工具并优化工作负荷](lesson-1-1-tuning-a-workload.md)  
  
  
