---
title: "如何： 调试自定义程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e33f560106e99062e89ec10bbe84de65a360118f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-debug-custom-assemblies"></a>如何调试自定义程序集
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]提供多个调试工具，可帮助你分析你的自定义程序集代码和在其中找到错误。 要使用的最佳工具取决于您试图完成的任务。 此示例使用 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]。  
  
 设计、开发和测试 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 自定义程序集的建议方式是创建包含您的测试报表和自定义程序集的解决方案。  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>使用 Visual Studio 的单个实例调试程序集  
  
1.  使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 创建新的报表项目。  
  
     创建报表项目时，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 还会创建一个用以包含该项目的解决方案。  
  
2.  将一个新的类库项目添加到现有解决方案。 请确保该报表项目设置为启动项目。 有关如何实现此操作的详细信息，请参阅 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文档。  
  
3.  在解决方案资源管理器中，选择解决方案。  
  
4.  上**视图**菜单上，单击**属性页**。  
  
     **解决方案属性页**对话框随即打开。  
  
5.  在左窗格中，展开**通用属性**如有必要，单击**项目依赖项**。 选择从报表项目**项目**下拉列表。 选择程序集的项目中**依赖于**列表。  
  
6.  单击**确定**以保存所做的更改，并关闭**属性页**对话框。  
  
7.  在解决方案资源管理器中，选择您的自定义程序集项目。  
  
8.  上**视图**菜单上，单击**属性页**。  
  
     **项目属性页**对话框随即打开。  
  
9. 单击**生成**选项卡上，如果你在 C# 项目或**编译**选项卡上，如果你在[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目。  
  
10. 上**生成**/**编译**页上，输入报表设计器文件夹的路径。 默认情况下，这是 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE） 中**输出路径**文本框。 这将在执行您的报表之前将自定义程序集的更新的版本直接生成和部署到报表设计器中。  
  
11. 在您设计了报表并开发了自定义程序集后，在自定义程序集代码中设置断点。  
  
12. 运行下的报表**DebugLocal**模式通过按 F5 键。 在报表在弹出式预览窗口中执行时，调试器命中与程序集中的可执行代码相对应的任何断点。 使用 F11 可以单步执行您的自定义程序集代码。  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>使用 Visual Studio 的两个实例调试程序集  
  
1.  启动 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 并打开您的自定义程序集项目。  
  
2.  生成项目，并将自定义程序集以及随附的 .pdb 文件部署到报表设计器。 有关部署的详细信息，请参阅[部署自定义程序集](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)。  
  
3.  打开使用您的自定义程序集的报表项目，同时在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的一个单独实例中让自定义程序集代码处于打开状态。  
  
4.  导航到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中包含自定义程序集项目的实例，并在代码中设置一些断点。  
  
5.  使用自定义程序集项目仍是活动的窗口中，单击**附加到进程**上**调试**菜单。  
  
     **附加到进程**对话框随即打开。  
  
6.  从进程的列表中，选择报表项目对应的 devenv.exe 进程，然后单击**附加**。  
  
7.  定义将用于您的自定义程序集的报表的表达式并设计报表。  
  
8.  在完成设计您的报表，请单击**预览**选项卡。  
  
     报表将执行，并且自定义程序集代码应在您预定义的断点处中断。  
  
    > [!NOTE]  
    >  使用**预览**选项卡不会强制代码程序集的权限。 为完整测试，其中包括任何代码访问安全错误，启动下的报表项目**DebugLocal**配置设置。  
  
9. 使用 F11 键分步执行代码。 有关使用调试的详细信息[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，请参阅[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]文档。  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
