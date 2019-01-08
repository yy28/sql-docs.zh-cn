---
title: 生成、部署和调试自定义对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22b7d07752c6a9df5f0b100c0d16b78a86125f04
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362849"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>生成、部署和调试自定义对象
  在为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的自定义对象编写代码后，必须生成和部署程序集，将该程序集集成到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，使其可在包中使用，然后对其进行测试和调试。  
  
##  <a name="top"></a> 生成、部署和调试 Integration Services 自定义对象的步骤  
 您已编写了对象的自定义功能代码。 现在必须对所编写的代码进行测试，使其可供用户使用。 对于可为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 创建的所有类型的自定义对象，步骤都非常相似。  
  
 下面是生成、部署和调试自定义对象应遵循的步骤：  
  
1.  使用强名称为要生成的程序集[签名](#signing)。  
  
2.  [生成](#building)程序集。  
  
3.  通过将程序集移动到或复制到适当的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 文件夹来[部署](#deploying)该程序集。  
  
4.  在全局程序集缓存 (GAC) 中[安装](#installing)该程序集。  
  
     此对象自动添加到工具箱中。  
  
5.  如有必要，对部署进行[故障排除](#troubleshooting)。  
  
6.  [测试](#testing)并调试代码。  
  
##  <a name="signing"></a> 为程序集签名  
 若要共享程序集，必须将其安装在全局程序集缓存中。 程序集被添加到全局程序集缓存之后，可以由 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 这样的应用程序使用。 全局程序集缓存要求必须使用强名称为程序集进行签名，这样可保证程序集是全局唯一的。 强名称程序集有一个完全限定的名称，由程序集的名称、区域性、公钥及版本号组成。 运行库使用这些信息来定位程序集并将其与其他同名的程序集区分开。  
  
 若要使用强名称为程序集签名，必须首先具有或创建公钥/私钥对。 这一对加密公钥和加密私钥用于在生成时创建强名称程序集。  
  
 有关强名称的详细信息和为程序集签名所必须遵循的步骤，请参阅 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的下列主题：  
  
-   强名称程序集  
  
-   创建密钥对  
  
-   使用强名称为程序集签名  
  
 在生成时，可以轻松在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中使用强名称为程序集签名。 在“项目属性”对话框中，选择“签名”选项卡。选择“为程序集签名”的选项，然后提供密钥文件 (.snk) 的路径。  
  
##  <a name="building"></a> 生成程序集  
 为项目签名后，必须使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的“生成”菜单上可用的命令来生成或重新生成项目或解决方案。 您的解决方案可能包含单独的自定义用户界面项目，该项目也必须使用强名称签名，并且可以同时生成。  
  
 执行下两个步骤（部署程序集并将其安装在全局程序集缓存中）的最简便方法是将这些步骤编写为 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中的生成后事件。 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 项目的项目属性的“编译”页和 C# 项目的“生成事件”页都提供可用的生成事件。 命令提示实用工具（如 gacutil.exe）需要完整路径。 包含空格的路径和展开为包含空格的路径的宏（如 $(TargetPath)）的前后都需要引号。  
  
 下面是自定义日志提供程序的生成后事件命令行的示例：  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\120\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a> 部署程序集  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器对安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 时创建的一系列文件夹中的文件进行枚举，从而查找可在包中使用的自定义对象。 当默认值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用安装设置，这一系列文件夹位于下**C:\Program Files\Microsoft SQL Server\120\DTS**。 但是如果为自定义对象创建安装程序，则应检查的值**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\Setup\DtsPath**注册表项以验证此位置文件夹。  
  
 可以通过下面两种方式将程序集放入文件夹中：  
  
-   在生成已编译的程序集后，将其移动或复制到相应的文件夹中。 （为方便起见，可以在生成后事件中包含复制命令。）  
  
-   直接在相应的文件夹中生成程序集。  
  
 下的下列部署文件夹**C:\Program Files\Microsoft SQL Server\120\DTS**用于各种类型的自定义对象：  
  
|自定义对象|部署文件夹|  
|-------------------|-----------------------|  
|任务|“任务”|  
|“ODBC 源编辑器”|连接|  
|日志提供程序|LogProviders|  
|数据流组件|PipelineComponents|  
  
> [!NOTE]  
>  将程序集复制到这些文件夹中即可支持可用任务、连接管理器等的枚举。 因此，您不一定要将只包含用于自定义对象的自定义用户界面的程序集部署到这些文件夹中。  
  
##  <a name="installing"></a> 在全局程序集缓存中安装程序集  
 若要将任务程序集安装到全局程序集缓存 (GAC) 中，请使用命令行工具 gacutil.exe，或将程序集拖至 `%system%\assembly` 目录中。 为方便起见，还可以在生成事件后中调用 gacutil.exe。  
  
 下面的命令使用 gacutil.exe 将名为 MyTask.dll 的组件安装到 GAC 中。  
  
 `gacutil /iF MyTask.dll`  
  
 在安装新版本的自定义对象后，必须先关闭再重新打开 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器。 如果已在全局程序集缓存中安装了早期版本的自定义对象，必须先删除这些对象再安装新版本。 若要卸载程序集，请运行 gacutil.exe 并在 `/u` 选项中指定程序集名称。  
  
 有关全局程序集缓存的详细信息，请参阅“[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 工具”中的“全局程序集缓存工具 (Gactutil.exe)”。  
  
##  <a name="troubleshooting"></a> 对部署进行故障排除  
 如果自定义对象显示在“工具箱”或可用对象列表中，但无法将其添加到包中，可以尝试以下操作：  
  
1.  在全局程序集缓存中查找该组件是否有多个版本。 如果全局程序集缓存中存在该组件的多个版本，则设计器可能无法加载该组件。 请删除全局程序集缓存中该程序集的所有实例，然后重新添加该程序集。  
  
2.  请确保部署文件夹中只存在一个程序集实例。  
  
3.  刷新工具箱。  
  
4.  将 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 附加到 devenv.exe，然后设置一个断点以单步执行初始化代码，确保不会发生异常。  
  
##  <a name="testing"></a> 测试并调试代码  
 若要调试自定义对象的运行时方法，最简单的方法是在生成自定义对象后从 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 启动 dtexec.exe，然后运行使用该组件的包。  
  
 如果你想要调试组件的设计时方法，如`Validate`方法中，打开第二个实例中使用该组件的包[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，并将附加到其**devenv.exe**过程。  
  
 如果还希望在包已打开并在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中运行时调试组件的运行时方法，必须在包的执行过程中强制暂停，以便还能够附加到 DtsDebugHost.exe 进程。  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>通过附加到 dtexec.exe 来调试对象的运行时方法  
  
1.  在调试配置中，按照本主题中的说明签名和生成项目，进行部署，然后安装到全局程序集缓存中。  
  
2.  上**调试**选项卡**项目属性**，选择**启动外部程序**作为**启动操作**，并找到**dtexec.exe**，这默认安装在 C:\Program Files\Microsoft SQL Server\120\DTS\Binn。  
  
3.  在“启动选项”下的“命令行选项”文本框中，输入运行使用了组件的包所需的命令行参数。 通常，命令行参数包含 /F[ILE] 开关，后跟 .dtsx 文件的路径和文件名。 有关详细信息，请参阅 [dtexec Utility](../packages/dtexec-utility.md)。  
  
4.  在组件的运行时方法源代码中根据需要设置断点。  
  
5.  运行您的项目。  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>通过附加到 SQL Server Data Tools 来调试自定义对象的设计时方法  
  
1.  在调试配置中，按照本主题中的说明签名和生成项目，进行部署，然后安装到全局程序集缓存中。  
  
2.  在自定义对象的设计时方法源代码中根据需要设置断点。  
  
3.  打开第二个 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例，并加载使用自定义对象的包所在的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
4.  从 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的第一个实例，附加到 devenv.exe 的第二个实例，其中包是通过从第一个实例的“调试”菜单选择“附加到进程”加载的。  
  
5.  从第二个 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例运行包。  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>通过附加到 SQL Server Data Tools 来调试自定义对象的运行时方法  
  
1.  完成上述过程中列出的步骤之后，在执行包时强制暂停，以便可附加到 DtsDebugHost.exe 中。 此强制暂停的方法是：向 `OnPreExecute` 事件添加断点，或向项目添加脚本任务并输入用于显示模式消息框的脚本。  
  
2.  运行包。 出现暂停时，切换到已在其中打开代码项目的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 实例，并从“调试”菜单中选择“附加到进程”。 请确保附加到在“类型”列中列为“托管，x86”的 DtsDebugHost.exe 实例，而不是只列为 x86 的实例。  
  
3.  返回到暂停的包，并继续通过断点，或单击“确定”来关闭脚本任务引发的消息框，并继续包的执行和调试。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>请参阅  
 [开发 Integration Services 的自定义对象](developing-custom-objects-for-integration-services.md)   
 [使自定义对象持久化](persisting-custom-objects.md)   
 [包开发的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
