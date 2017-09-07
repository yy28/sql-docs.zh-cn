---
title: "引用脚本解决方案中的其他程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>引用脚本解决方案中的其他程序集
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]类库提供用于实现中的自定义功能的脚本开发人员，使用一套强大的工具[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]包。 脚本任务和脚本组件还可以使用自定义托管程序集。  
  
> [!NOTE]  
>  若要启用你的包以使用的对象和从 Web 服务的方法，使用**添加 Web 引用**命令中提供[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的早期版本中，必须生成代理类才能使用 Web 服务。  
  
## <a name="using-a-managed-assembly"></a>使用托管程序集  
 有关[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]若要查找在设计时的托管程序集，必须执行以下步骤：  
  
1.  将托管程序集存储在计算机上的任何文件夹中。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的早期版本中，只能添加对存储在 %windir%\Microsoft.NET\Framework\vx.x.xxxxx 文件夹或 %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies 文件夹中的托管程序集的引用。  
  
2.  添加对托管程序集的引用。  
  
     若要添加的引用，在 VSTA，在**添加引用**对话框中，在**浏览**选项卡上，找到并添加的托管程序集。  
  
 对于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，若要在运行时查找托管程序集，必须执行以下步骤：  
  
1.  用强名称为托管程序集签名。  
  
2.  将程序集安装到运行包的计算机的全局程序集缓存中。  
  
     有关详细信息，请参阅[构建，Deploying，and Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>使用 Microsoft .NET Framework 类库  
 脚本任务和脚本组件能够利用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类库公开的所有其他对象和功能。 例如，使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 可以检索有关环境的信息，并与运行包的计算机进行交互。  
  
 下表介绍了一些比较常用的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类：  
  
-   **System.Data**包含 ADO.NET 体系结构。  
  
-   **System.IO**提供与文件系统和流的接口。  
  
-   **System.Windows.Forms**提供窗体创建。  
  
-   **System.Text.RegularExpressions**提供用于使用正则表达式的类。  
  
-   **System.Environment**返回有关本地计算机、 当前用户和计算机和用户设置的信息。  
  
-   **System.Net**提供网络通信。  
  
-   **System.DirectoryServices**公开 Active Directory。  
  
-   **System.Drawing**提供了大量图像操作库。  
  
-   **System.Threading**能够多线程的编程。  
  
 有关 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的详细信息，请参阅 MSDN Library。  
  
## <a name="see-also"></a>另请参阅  
 [使用脚本扩展包](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
