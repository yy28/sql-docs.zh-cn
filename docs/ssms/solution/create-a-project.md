---
title: 创建项目 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.newproject
- vs.addnewproject
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b9549bfce672b3ddf5c67ddb8a6a4968e87a5b7
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2018
ms.locfileid: "42776172"
---
# <a name="create-a-project"></a>创建项目
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可以在现有解决方案中创建一个或多个项目。  
  
### <a name="to-create-a-new-project-and-add-it-to-a-solution"></a>创建一个新项目并将其添加到解决方案中  
  
1.  在解决方案资源管理器中，选择解决方案。  
  
2.  在“文件”菜单中，指向“添加”，再单击“新建项目”。  
  
3.  在“新建项目”对话框中，单击一个项目类型。  
  
    **模板**  
    在“模板”框中，选择一个模板。 在“模板”框下会显示所选项目模板的简短说明。  
  
    **名称**  
    输入要创建的脚本项目的名称。 同时将会在“位置”字段中显示的位置创建一个与项目同名的文件夹。 对于某些项目，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将创建源文件和其他支持文件，并将其添加到新项目文件夹中。  
  
    > [!NOTE]  
    > 对于某些项目类型，由于指定位置即设置了名称，所以“名称”文本框不可用。 例如，Web 应用程序和 Web 服务位于 Web 服务器上，因此它们的名称都取自其所在服务器上指定的虚拟目录。  
  
    名称不能包含下列字符：  
  
    -   井号 (#)  
  
    -   百分号 (%)  
  
    -   与符号 (&)  
  
    -   星号 (*)  
  
    -   竖线 (|)  
  
    -   反斜杠 (\\)  
  
    -   冒号 (:)  
  
    -   引号 (")  
  
    -   小于号 (\<)  
  
    -   大于号 (>)  
  
    -   问号 (?)  
  
    -   正斜杠 (/)  
  
    -   前导空格或尾随空格 (' ')  
  
    -   为 Microsoft Windows 或 MS-DOS 保留的名称，如（“nul”、“aux”、“con”、“com1”、“lpt1”等）  
  
    **位置**  
    输入要创建项目的位置，或者从列表中选择位置。  
  
    **“浏览”**  
    显示“项目位置”对话框，使用该对话框，可以导航到一个保存项目的新目录。  
  
    **解决方案**  
    选择“创建新的解决方案”在“解决方案资源管理器”中创建一个解决方案。 选择“添加到解决方案”将新项目添加到“解决方案资源管理器”当前打开的解决方案。  
  
    **创建解决方案的目录**  
    选择启用“(解决方案)名称”文本框。 此选项会创建一个新的目录，其名称是您为项目和解决方案选择的名称。  
  
    **解决方案名称**  
    输入要在其中创建项目的新解决方案的名称。 默认情况下，此字段使用的名称与在“名称”字段中输入的名称相同。  
  
    **注意**若要访问此选项，必须同时选中“解决方案”中的“创建新的解决方案”复选框和“创建解决方案的目录”复选框。 某些项目模板不支持此选项，例如 Web 应用程序。  
  
    **添加到源代码管理**  
    选中此复选框后，在单击“确定”时即会打开源代码管理应用程序。 填写源代码管理应用程序所要求的所有信息以继续进行操作。 必须安装源代码管理客户端应用程序才能使用此选项。  
  
4.  单击“确定” 。  
  
您可以设置脚本项目的名称，但文件夹名称则由 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 确定，并且不能更改。 可以使用“添加新项目”对话框，为一组公共文件夹配置驱动器和路径说明。 右键单击“解决方案资源管理器”中的解决方案图标，再单击“添加”。 脚本项目文件夹的默认位置是 C:\Documents and Settings\\*username*\My Documents\SQL Server Management Studio\Projects\\。  
  
## <a name="see-also"></a>另请参阅  
[解决方案资源管理器](../../ssms/solution/solution-explorer.md)  
[在解决方案中添加现有项目](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[向项目添加新项](../../ssms/solution/add-new-items-to-a-project.md)  
[向项目中添加现有项](../../ssms/solution/add-existing-items-to-a-project.md)  
[更改项目的默认位置](../../ssms/solution/change-the-default-location-for-projects.md)  
[移除或删除项或项目](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[删除解决方案](../../ssms/solution/delete-a-solution.md)  
  
