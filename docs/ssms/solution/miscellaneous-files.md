---
title: 杂项文件 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: ca1a2d705c7d5f7808ee8c83f014bcb734f9f151
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67689815"
---
# <a name="miscellaneous-files"></a>杂项文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
不属于任何项目的文件称为杂项文件  。 当您打开解决方案时，可以打开并修改与该项目相关的杂项文件。 如果文件扩展名与项目代码编辑器不关联，则将此文件归类为杂项文件。 例如，在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目中，扩展名为 .txt 或 .mdx 的文件被视为杂项文件。 在 MDX 项目中，扩展名为 .txt 或 .sql 的文件被视为杂项文件。 若要使文件扩展名与代码编辑器相关联，请参阅[如何：将文件扩展名关联到代码编辑器](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
为项目添加杂项文件的功能非常有用，许多理由都可以说明这一点。 您的某个文件可能是无需识别的脚本，但却是解决方案开发中不可缺少的一部分。 常见示例包括开发注释或说明、数据文件和代码片段。  
  
杂项文件可提供灵活性。 例如，假定有一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目，该项目具有多个用于在数据库中创建表和存储过程的脚本。 还有几个文件扩展名为 .BCP 的用于表的数据文件，以及一个包括执行说明的 README.TXT 文件。 您可以将数据文件和 README 文件作为杂项文件附加到项目中，以利用项目系统的源代码管理和其他功能。  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 菜单和工具栏会随打开的文件的格式而改变。 例如，打开文本文件时，会显示文本编辑器工具栏。 如果打开 XML 架构文件，则显示 XML 架构工具栏。 编辑 XML 架构时，文本编辑器工具栏将不可用。 在项目文件和杂项文件之间切换时，与项目相关的所有命令和工具栏均被与杂项文件相关的命令和工具栏取代。  
  
## <a name="see-also"></a>另请参阅  
[用于管理解决方案和项目的文件](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[解决方案 (SQL Server Management Studio)](../../ssms/solution/solutions-sql-server-management-studio.md)  
[项目 (SQL Server Management Studio)](../../ssms/solution/projects-sql-server-management-studio.md)  
  
