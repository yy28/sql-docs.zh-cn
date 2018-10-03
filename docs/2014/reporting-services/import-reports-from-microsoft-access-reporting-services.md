---
title: 从 Microsoft Access (Reporting Services) 导入报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc63daf4095238f948be6bde22bf190aa4d1977a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086499"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>从 Microsoft Access 导入报表 (Reporting Services)
  在报表设计器中，你可以导入报表从[!INCLUDE[msCoName](../includes/msconame-md.md)]访问数据库或项目。 必须在安装报表设计器的计算机上安装 Access 2002 或更高版本。  
  
 使用导入功能时，将导入数据库或项目文件中的所有报表。 如果 Access 文件中包含多个报表，您可能需要创建一个单独的报表项目，以便将报表导入到其中，然后在主报表项目中打开各个 RDL 文件。 将报表导入到报表设计器后，可以对报表进行编辑。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 并不支持所有的 Access 报表对象。 不转换的项以显示**任务列表**窗口。 有关详细信息，请参阅[支持的 Access 报表功能&#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md)。  
  
### <a name="to-import-reports-from-microsoft-access"></a>若要从 Microsoft Access 导入报表  
  
1.  打开或创建一个项目，报表将导入其中。  
  
2.  上**项目**菜单，依次指向**导入报表**，然后单击**Microsoft Access**。 或者，右键单击解决方案资源管理器中的项目，指向**导入报表**，然后单击**Microsoft Access**。  
  
3.  在中**开放**对话框框中，选择 Access 数据库 （.mdb、.accdb） 或项目 (.adp)，包含报表，然后单击**打开**。 数据库或项目文件中的所有报表将被导入，并在解决方案资源管理器的“报表”文件夹中列出。  
  
4.  检查**任务列表**窗口生成错误。 若要查看**任务列表**窗口中，打开**视图**菜单上，指向**其他 Windows**，然后单击**任务列表**。  
  
## <a name="see-also"></a>请参阅  
 [使用报表设计器设计报表 (SSRS)](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
