---
title: SQL Server 参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine analysis [Upgrade Advisor]
- SQL Server Upgrade Advisor, Database Engine
- Upgrade Advisor [SQL Server], Database Engine
- analyzing system [Upgrade Advisor], Database Engine
ms.assetid: 44a18bfe-e593-47a5-995f-382c01d3f618
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e528b94e51238a06a9776e58693c3093f4bfb831
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091880"
---
# <a name="sql-server-parameters"></a>SQL Server 参数
  在该页上，设置分析器将用于[!INCLUDE[ssDE](../../includes/ssde-md.md)]分析的参数。 您可以分析一个、多个或所有数据库，分析通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]创建的跟踪文件，以及 SQL 批处理文件。  
  
> [!NOTE]  
>  只有提交要分析的跟踪文件或 SQL 批处理文件时，才能检测到某些升级问题。  
  
## <a name="options"></a>选项  
 **要分析的数据库**  
 若要分析所有数据库，请选中 "**所有数据库**" 复选框。 若要分析多个数据库，请选中相应的每个数据库旁边的复选框以将其包括在扫描范围内。  
  
 **分析跟踪文件**  
 选中此复选框可分析文件系统中的跟踪文件。  
  
 **跟踪文件的路径**  
 可分析一个或多个文件。 您可以浏览到某个位置并选择多个文件，也可以提供多个文件名。 请使用每个文件的完整路径名，将文件名包括在内，并用竖线字符 (|) 分隔各项。  
  
 如果启用 "**分析跟踪文件**"，则在输入路径名称和文件名之前，将禁用 "**下一步**"。  
  
 **分析[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批处理文件**  
 选中此复选框可分析文件系统中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理文件。  
  
 **批处理文件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的路径**  
 可分析一个或多个批处理文件。 可先浏览到某个位置然后选择多个文件，或者可提供多个文件名。 请使用每个文件的完整路径名，将文件名包括在内，并用竖线字符 (|) 分隔各项。  
  
 如果启用 "**分析 SQL 批处理文件**"，则在输入路径名称和文件名之前，"**下一步**" 按钮处于禁用状态。  
  
 **SQL 批处理分隔符**  
 用于分隔成批的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的文本。 默认值为 "**开始**"。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
