---
title: 管理使用编码的文件
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 67106a11e7a42f6167c0d08df99917ed057f11f5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75251879"
---
# <a name="manage-files-with-encoding"></a>管理使用编码的文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
为便于以特定语言显示代码以及在特定平台中显示代码，可以将特定的字符编码与文件关联。  
  
## <a name="opening-files"></a>打开文件  
可以选择用于编辑文件的编辑器。  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>用特定的编辑器打开文件  
  
1.  在“文件”  菜单中，指向“打开”  ，再单击“文件”  。  
  
2.  在“打开文件”  对话框中，选择文件名。  
  
3.  单击“打开”  按钮旁边的箭头，再从显示的菜单中单击“打开方式”  。  
  
4.  在“选择要打开的程序”  列表中，选择一种编辑器，再单击“打开”  。 若要用特定的编码打开文件，请选择提供编码支持的编辑器（如使用编码的 SQL 查询编辑器或使用编码的 XML 编辑器）。  
  
## <a name="saving-files"></a>保存文件  
也可以用 Unicode 编码或其他代码页保存代码，以支持各种语言，如西欧或东欧语言。 可以将特定的字符编码与文件关联，以便于以该语言显示代码；也可以将特定的字符编码与行尾类型关联，以支持特定的操作系统。 此外，某些字符如果被用在文件名中，则只有使用 Unicode 编码才能保存这些字符。  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>用其他编码或行尾类型保存文件  
  
1.  在“文件”  菜单上，单击“将  **另存为”<filename>** 。  
  
2.  在“文件另存为”  对话框中，展开“保存”  按钮，再单击“编码保存”  。  
  
3.  从“高级保存选项”  对话框的“编码”  列表中，选择所需的编码。  
  
4.  从“行尾”  列表中，选择所需的行尾类型。  
  
    > [!NOTE]  
    > 如果用 Unicode 编码保存文件，则该文件应作为二进制文件签入 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual SourceSafe，因为 Visual SourceSafe 不支持对保存为 Unicode 的文件间的差异进行合并、比较和显示。  
  
如果您使用 Visual SourceSafe 并以 ANSI、UTF8 或 Unicode 存储文件，请注意以下各种编码的限制：  
  
-   ANSI 文件仅允许使用当前代码页中支持的字符，这将限制国际化的使用。  
  
-   Unicode 文件是作为二进制文件处理的，因此不能以共享方式签出、进行差异检查或合并功能。 可以在国际化文件中使用此格式。  
  
-   UTF8 文件不能在 Visual SourceSafe 中安全使用，因为在签入、签出、差异检查和合并过程中，会产生导致 UTF8 文件编辑器出现问题的更改。  
  
## <a name="see-also"></a>另请参阅  
[用于管理解决方案和项目的文件](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[将文件扩展名与代码编辑器关联](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
