---
title: "将文件扩展名与代码编辑器关联 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file extensions [SQL Server]
- associating file extensions [SQL Server]
- Query Editor [SQL Server Management Studio], associating file extensions
ms.assetid: 193630f4-93de-4950-8f36-68702531f925
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c46c2a4eee1f3acc1f33c276e707cb21f4312672
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="associate-file-extensions-to-a-code-editor"></a>将文件扩展名与代码编辑器关联
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]将文件扩展名与特定代码编辑器关联，可通过在 Windows 资源管理器中双击文件，使用相应的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 代码编辑器打开文件。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的常用扩展名（例如 .sql 和 .mdx）是在安装过程中关联的。 新的文件扩展名也必须在文件系统中与 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 相关联。 使用此功能可以打开通过其他编辑器创建的文件，也可以打开重命名的文件，例如重命名为 .bak 的 .sql 文件的备份。  
  
 关联过程分为两步。 首先将扩展名与 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]相关联，然后将扩展名与特定代码编辑器相关联。  
  
### <a name="to-associate-a-new-file-extension-with-sql-server-management-studio"></a>将新的文件扩展名与 SQL Server Management Studio 相关联  
  
1.  在 **“开始”** 菜单中，指向 **“所有程序”**，指向 **“附件”**，再单击 **“Windows 资源管理器”**。  
  
2.  在 Windows 资源管理器的 **“工具”** 菜单上，单击 **“文件夹选项”**。  
  
3.  在 **“文件夹选项”** 对话框的 **“文件类型”** 选项卡上，单击 **“新建”**。  
  
4.  在 **“新建扩展名”** 对话框的 **“文件扩展名”** 框中，键入要关联的新文件扩展名，然后单击 **“确定”**。 扩展名不要以句点开头。  
  
5.  在 **“已注册的文件类型”** 框，单击新的扩展名，再单击 **“更改”**。  
  
6.  在 **“打开方式”** 对话框中，单击 **“SSMS – SQL Server Management Studio”**，再单击 **“确定”**。  
  
7.  单击 **“关闭”** 关闭 **“文件夹选项”** 对话框，然后关闭 Windows 资源管理器。  
  
### <a name="to-associate-a-new-file-extension-with-a-code-editor-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中将新文件扩展名与代码编辑器相关联  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **“工具”** 菜单中，单击 **“选项”**。  
  
2.  在 **“选项”** 对话框中，单击 **“文本编辑器”**，再单击 **“文件扩展名”**。  
  
3.  在 **“扩展名”** 框中，键入新的文件扩展名。  
  
4.  在 **“编辑器”** 框中，单击要用于打开此文件类型的代码编辑器，单击 **“添加”**，再单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [Ssms 实用工具](../../tools/sql-server-management-studio/ssms-utility.md)  
  
  
