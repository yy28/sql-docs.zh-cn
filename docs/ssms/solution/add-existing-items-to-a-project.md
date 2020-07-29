---
title: 向项目中添加现有项
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 60939da70ed334f4fc7c020f123fff9441a27088
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003312"
---
# <a name="add-existing-items-to-a-project"></a>向项目中添加现有项
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
向项目中添加新项，以扩展应用程序功能。 现有项可以是查询，也可以是杂项文件。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 有两个项目类型： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目和 Analysis Services 脚本项目。 至于哪些查询文件可以添加到项目中，则取决于项目类型。 例如，可以将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询（扩展名为 .sql 的文件）添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目，但是不能将其添加到 Analysis Services 脚本项目。 若要将附加文件扩展名关联到项目类型，请参阅 [如何将文件扩展名与代码编辑器关联](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>向项目中添加现有查询或杂项文件  
  
1.  在解决方案资源管理器中，选择目标项目。  
  
2.  在“项目”  菜单上，单击“添加现有项”  。  
  
    **Look in**  
    找到要从此列表添加到项目中的文件或文件夹。 对于 XML Web services 和 ASP.NET Web 应用程序，文件位于 Web 服务器上。  
  
    **桌面**  
    显示桌面上的文件和文件夹。  
  
    **我的项目**  
    显示默认“我的项目”  位置中的文件和文件夹。  
  
    **我的电脑**  
    显示“我的电脑”  文件夹的内容。  
  
    **文件名**  
    使用此选项可以筛选所显示的文件和文件夹。 输入要用来筛选的完整或部分文件名，使用星号 (`*`) 作为通配符。  
  
    > [!NOTE]  
    > 通过在“文件名”  框中输入 URL 或网络路径，导航到 Web 和网络位置。 例如，输入 `https://mywebsite` 可显示 mywebsite Web 位置中可用的文件，输入 \\\myserver\myshare 可显示 myserver 上的 myshare 位置中可用的文件。  
  
    **文件类型**  
    使用此选项基于文件扩展名筛选文件。 每个产品列出最常用文件类型的默认筛选器。  
  
    **添加**  
    使用此下拉按钮可以向项目中添加项以及在默认编辑器中打开该项。  
  
    -   **添加**  
  
        将现有项复制到磁盘上的项目文件夹，并添加解决方案资源管理器中选定项目下的项。 对该项所做的任何更改没有反映原始位置中的项。 这是该文件类型的默认编辑器。  
  
    -   **添加为链接**  
  
        向项目中添加所选文件，并以该文件类型的默认编辑器打开文件。 该选项将打开最初选定的文件，而不将文件复制到项目文件夹中。  
  
3.  如果添加查询文件，则“连接”对话框将提示您为查询指定连接。 如果不希望将连接关联到查询，则可以单击“连接”对话框中的“取消”  。  
  
4.  该文件将添加到项目的“查询”  或“杂项文件”  文件夹中。  
  
## <a name="see-also"></a>另请参阅  
[解决方案资源管理器](../../ssms/solution/solution-explorer.md)  
[向项目添加新项](../../ssms/solution/add-new-items-to-a-project.md)  
[移除或删除项或项目](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
