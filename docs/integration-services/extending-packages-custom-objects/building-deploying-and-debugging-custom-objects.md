---
title: "生成、 部署和调试自定义对象 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>生成、部署和调试自定义对象
  在编写的自定义对象的代码后[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，必须生成的程序集、 部署该环节，并将其到集成[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器以使其在包中，可供使用和测试，并对其进行调试。  
  
##  <a name="top"></a>在生成、 部署和调试 Integration services 的自定义对象中的步骤  
 您已编写了对象的自定义功能代码。 现在必须对所编写的代码进行测试，使其可供用户使用。 对于可为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 创建的所有类型的自定义对象，步骤都非常相似。  
  
 下面是生成、 部署和对其进行测试的步骤。  
  
1.  [登录](#signing)生成具有强名称的程序集。  
  
2.  [生成](#building)程序集。  
  
3.  [部署](#deploying)对程序集进行移动或复制到相应[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]文件夹。  
  
4.  [安装](#installing)全局程序集缓存 (GAC) 中的程序集。  
  
     此对象自动添加到工具箱中。  
  
5.  [解决](#troubleshooting)部署，如有必要。  
  
6.  [测试](#testing)和调试你的代码。  
  
 你可以现在使用 SSIS 设计器在 SQL Server Data Tools (SSDT) 来创建、 维护和运行面向不同版本的包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关的影响的自定义扩展此改进的详细信息，请参阅[获取 SSIS 自定义扩展以支持的 SQL Server 2016 SSDT 2015 的多版本支持](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>对程序集签名  
 若要共享程序集，必须将其安装在全局程序集缓存中。 程序集被添加到全局程序集缓存之后，可以由 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 这样的应用程序使用。 全局程序集缓存要求必须使用强名称为程序集进行签名，这样可保证程序集是全局唯一的。 强名称程序集有一个完全限定的名称，由程序集的名称、区域性、公钥及版本号组成。 运行库使用这些信息来定位程序集并将其与其他同名的程序集区分开。  
  
 若要使用强名称为程序集签名，必须首先具有或创建公钥/私钥对。 这一对加密公钥和加密私钥用于在生成时创建强名称程序集。  
  
 有关强名称的详细信息和为程序集签名所必须遵循的步骤，请参阅 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的下列主题：  
  
-   强名称的程序集  
  
-   创建密钥对  
  
-   使用强名称为程序集签名  
  
 在生成时，可以轻松在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中使用强名称为程序集签名。 在**项目属性**对话框中，选择**签名**选项卡。 选择该选项以**对程序集签名**然后提供密钥 (.snk) 文件的路径。  
  
##  <a name="building"></a>生成程序集  
 项目后，你必须生成或使用上的可用命令重新生成项目或解决方案**生成**菜单[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。 您的解决方案可能包含单独的自定义用户界面项目，该项目也必须使用强名称签名，并且可以同时生成。  
  
 下两个步骤是部署程序集并将其安装在全局程序集缓存中，执行这两个步骤最简便的方法是编写这些步骤的脚本，作为 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的生成后事件。 生成事件均从可用**编译**个项目属性页[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目，并从**生成事件**C# 项目的页。 完整路径，才能使用命令提示符实用工具，如**gacutil.exe**。 包含空格的路径和展开为包含空格的路径的宏（如 $(TargetPath)）的前后都需要引号。  
  
 下面是自定义日志提供程序的生成后事件命令行的示例：  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>部署程序集  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器通过枚举的一系列时，会创建的文件夹中找到的文件在包中查找可供使用的自定义对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安装。 当默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装设置，则该文件夹集合中的位于**C:\Program Files\Microsoft SQL Server\130\DTS**。 不过如果你自定义对象创建的安装程序，你应该检查的值**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath**注册表项以验证此文件夹的位置。  
  
> [!NOTE]  
>  有关如何部署自定义组件以很好地使用 SQL Server Data Tools 中的多版本支持的信息，请参阅[获取 SSIS 自定义扩展以支持的 SQL Server 2016 SSDT 2015 的多版本支持](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)。  
  
 可以通过下面两种方式将程序集放入文件夹中：  
  
-   在生成已编译的程序集后，将其移动或复制到相应的文件夹中。 （为方便起见，可以在生成后事件中包含复制命令。）  
  
-   直接在相应的文件夹中生成程序集。  
  
 下的以下部署文件夹**C:\Program Files\Microsoft SQL Server\130\DTS**各种类型的自定义对象的使用：  
  
|自定义对象|部署文件夹|  
|-------------------|-----------------------|  
|任务|“任务”|  
|“ODBC 目标编辑器”|连接|  
|日志提供程序|LogProviders|  
|数据流组件|PipelineComponents|  
  
> [!NOTE]  
>  将程序集复制到这些文件夹中即可支持可用任务、连接管理器等的枚举。 因此，您不一定要将只包含用于自定义对象的自定义用户界面的程序集部署到这些文件夹中。  
  
##  <a name="installing"></a>在全局程序集缓存中安装该程序集  
 若要将任务程序集安装到全局程序集缓存 (GAC) 中，使用命令行工具**gacutil.exe**，或拖动到的程序集`%system%\assembly`目录。 为方便起见，您还可以包含对的调用**gacutil.exe**后期生成事件中。  
  
 以下命令安装一个名为组件*MyTask.dll*到使用 GAC **gacutil.exe**。  
  
 `gacutil /iF MyTask.dll`  
  
 在安装新版本的自定义对象后，必须先关闭再重新打开 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器。 如果已在全局程序集缓存中安装了早期版本的自定义对象，必须先删除这些对象再安装新版本。 若要卸载程序集，运行**gacutil.exe**并指定与程序集名称`/u`选项。  
  
 有关全局程序集缓存的详细信息，请参阅“[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 工具”中的“全局程序集缓存工具 (Gactutil.exe)”。  
  
##  <a name="troubleshooting"></a>部署疑难解答  
 如果你自定义对象中出现**工具箱**或列表的可用对象中，但你不能将它添加到包，请尝试以下：  
  
1.  在全局程序集缓存中查找该组件是否有多个版本。 如果全局程序集缓存中存在该组件的多个版本，则设计器可能无法加载该组件。 请删除全局程序集缓存中该程序集的所有实例，然后重新添加该程序集。  
  
2.  请确保部署文件夹中只存在一个程序集实例。  
  
3.  刷新工具箱。  
  
4.  附加[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]到**devenv.exe**和设置断点，以单步执行初始化代码以确保没有异常产生。  
  
##  <a name="testing"></a>测试和调试你的代码  
 调试自定义对象的运行时方法的最简单方法是从开始**dtexec.exe**从[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]后生成自定义对象和运行使用该组件的包。  
  
 如果你想要调试的组件的设计时方法，例如**验证**方法中，打开它的第二个实例中使用的组件中的包[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，并附加到其**devenv.exe**过程。  
  
 如果你还想要调试包是打开且运行时组件的运行时方法[!INCLUDE[ssIS](../../includes/ssis-md.md)]设计器中，你必须强制包执行过程中的暂停，以便你也可以附加到**DtsDebugHost.exe**过程。  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>通过附加到 dtexec.exe 来调试对象的运行时方法  
  
1.  在调试配置中，按照本主题中的说明签名和生成项目，进行部署，然后安装到全局程序集缓存中。  
  
2.  上**调试**选项卡**项目属性**，选择**启动外部程序**作为**启动操作**，并找到**dtexec.exe**，这默认安装在 C:\Program Files\Microsoft SQL Server\130\DTS\Binn。  
  
3.  在**命令行选项**文本中，在**启动选项**，输入运行使用你的组件的包所需的命令行自变量。 通常，命令行参数包含 /F[ILE] 开关，后跟 .dtsx 文件的路径和文件名。 有关详细信息，请参阅 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。  
  
4.  在组件的运行时方法源代码中根据需要设置断点。  
  
5.  运行您的项目。  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>通过附加到 SQL Server Data Tools 来调试自定义对象的设计时方法  
  
1.  在调试配置中，按照本主题中的说明签名和生成项目，进行部署，然后安装到全局程序集缓存中。  
  
2.  在自定义对象的设计时方法源代码中根据需要设置断点。  
  
3.  打开第二个 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例，并加载使用自定义对象的包所在的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
4.  第一个实例从[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，将附加到的第二个实例**devenv.exe**中通过选择加载的包**附加到进程**从**调试**菜单中的第一个实例。  
  
5.  从第二个 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例运行包。  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>通过附加到 SQL Server Data Tools 来调试自定义对象的运行时方法  
  
1.  完成前面的过程中列出的步骤后，强制你的包执行过程中暂停，以便可以将附加到**DtsDebugHost.exe**。 你可以通过添加到断点强制此暂停**OnPreExecute**事件，或通过将脚本任务添加到你的项目，并输入显示一个模式的消息框的脚本。  
  
2.  运行包。 暂停时，切换到的实例[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]中打开，并选择你的代码项目的即**附加到进程**从**调试**菜单。 请确保将附加到的实例**DtsDebugHost.exe**列为**托管，x86**中**类型**列，不属于列为实例**x86**仅。  
  
3.  返回到暂停包并跳过了断点，或单击**确定**关闭脚本任务中，引发的消息框并继续包执行和调试。  
  
## <a name="see-also"></a>另请参阅  
 [Integration services 的开发自定义对象](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [保持的自定义对象](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [包开发的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
