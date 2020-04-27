---
title: 创建存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62703092"
---
# <a name="creating-stored-procedures"></a>创建存储过程
  所有存储过程必须与公共语言运行时 (CLR) 或组件对象模型 (COM) 类相关联才能使用。 该类必须安装在服务器上（通常以[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX®动态链接库（DLL）的形式），并在服务器或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库中注册为程序集。  
  
 存储过程将在服务器或数据库中注册。 服务器存储过程可以从任何查询上下文进行调用。 而只有当数据库上下文是定义存储过程时所针对的数据库时，才能访问数据库存储过程。 如果一个程序集内的函数调用了另一个程序集内的函数，则必须在相同的上下文（服务器或数据库）中注册这两个程序集。 对于服务器或服务器上的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]已部署数据库，可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]来注册程序集。 对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 设计器在项目中注册程序集。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
## <a name="registering-a-server-assembly"></a>注册服务器程序集  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的对象资源管理器中，服务器程序集列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例下面的“程序集”文件夹中。 服务器程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-server-assembly"></a>创建服务器程序集  
  
1.  在对象资源管理器中展开的实例，右键单击 "**程序集**" 文件夹，然后单击 "**新建程序集**"。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 这会显示 "**注册服务器程序集**" 对话框。  
  
2.  对于**类型**，指定程序集的类型：  
  
    -   对于托管代码 (CLR) DLL，请指定 .NET 程序集。  
  
    -   对于本机代码（COM） DLL，请指定 COM DLL。  
  
3.  对于 "**文件名**"，请指定包含存储过程的 DLL。  
  
4.  对于 "**程序集名称**"，请指定程序集的名称。  
  
5.  如果这是要用于调试存储过程的库的调试版本，请选中 "**包括调试信息**" 复选框。 有关调试存储过程的详细信息，请参阅[调试存储过程](debugging-stored-procedures.md)。  
  
6.  您可以单击 **"确定"** 以立即注册程序集，或在对话框工具栏上单击 "**脚本**" 菜单上的命令，以将注册操作编写为查询窗口、文件或剪贴板的脚本。  
  
 注册服务器程序集之后，可以通过在对象资源管理器中右键单击该程序集，然后单击 "**属性**" 来配置该程序集。  
  
## <a name="registering-a-database-assembly-on-the-server"></a>在服务器上注册数据库程序集  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的对象资源管理器中，数据库程序集将列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库下面的“程序集”文件夹中。 数据库程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>在服务器上创建数据库程序集  
  
1.  在对象资源管理器中展开[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库实例，右键单击 "**程序集**" 文件夹，然后单击 "**新建程序集**"。 这会显示 "**注册数据库程序集**" 对话框。  
  
2.  对于**类型**，指定程序集的类型：  
  
    -   对于托管代码 (CLR) DLL，请指定 .NET 程序集。  
  
    -   对于本机代码 (COM) DLL，请指定 COM DLL。  
  
3.  对于 "**文件名**"，请指定包含存储过程的 DLL。  
  
4.  对于 "**程序集名称**"，请指定程序集的名称。  
  
5.  如果这是要用于调试存储过程的库的调试版本，请选中 "**包括调试信息**" 复选框。 有关调试存储过程的详细信息，请参阅[调试存储过程](debugging-stored-procedures.md)。  
  
6.  您可以单击 **"确定"** 以立即注册程序集，或在对话框工具栏上单击 "**脚本**" 菜单上的命令，以将注册操作编写为查询窗口、文件或剪贴板的脚本。  
  
 注册数据库程序集之后，可以通过在对象资源管理器中右键单击该程序集，然后单击 "**属性**" 来配置该程序集。  
  
## <a name="registering-a-database-assembly-in-a-project"></a>在项目中注册数据库程序集  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的解决方案资源管理器中，数据库程序集列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目下面的“程序集”文件夹中。 数据库程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>在 Analysis Service 项目中创建数据库程序集  
  
1.  在对象资源管理器中展开[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库实例，右键单击 "**程序集**" 文件夹，然后单击 "**新建程序集引用**"。 此时将显示 "**添加引用**" 对话框。 "**添加引用**" 对话框的 " **.net** " 选项卡列出现有的 .net （CLR）程序集，而 "**项目**" 选项卡列出项目。  
  
2.  您可以单击现有的组件或项目，然后单击 "**添加**" [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以将其添加到项目。 若要添加对 COM DLL 的引用，请单击 "**浏览**" 选项卡查找该文件。 "**选定的项目和组件**" 列表显示你要添加到项目中的每个组件的名称、类型、版本和位置。  
  
3.  完成选择要添加的组件后，单击 **"确定"** 将其添加到[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。  
  
## <a name="script-format-for-an-assembly"></a>程序集的脚本格式  
 注册 .NET 程序集的操作相当简单。 .NET 程序集将使用以下格式以二进制格式添加到数据库：  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](defining-stored-procedures.md)  
  
  
