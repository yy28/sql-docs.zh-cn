---
title: "创建存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a18ccef8d4e2e79f5a88e43def0bf13b683e266
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-stored-procedures"></a>创建存储的过程
  所有存储过程必须与公共语言运行时 (CLR) 或组件对象模型 (COM) 类相关联才能使用。 必须在服务器上安装类-通常在窗体的[!INCLUDE[msCoName](../../includes/msconame-md.md)]ActiveX® 动态链接库 (DLL) — 并为在服务器上或程序集已注册[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。  
  
 存储过程将在服务器或数据库中注册。 服务器存储过程可以从任何查询上下文进行调用。 而只有当数据库上下文是定义存储过程时所针对的数据库时，才能访问数据库存储过程。 如果一个程序集内的函数调用了另一个程序集内的函数，则必须在相同的上下文（服务器或数据库）中注册这两个程序集。 对于服务器或已部署[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库在服务器上，你可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]注册程序集。 对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 设计器在项目中注册程序集。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
## <a name="registering-a-server-assembly"></a>注册服务器程序集  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的对象资源管理器中，服务器程序集列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例下面的“程序集”文件夹中。 服务器程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-server-assembly"></a>创建服务器程序集  
  
1.  展开的实例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在对象资源管理器，右键单击**程序集**文件夹，，然后单击**新程序集**。 此时将显示**注册服务器程序集**对话框。  
  
2.  有关**类型**指定程序集的类型：  
  
    -   对于托管代码 (CLR) DLL，请指定 .NET 程序集。  
  
    -   对于本机代码 (COM) DLL，指定 COM DLL。  
  
3.  有关**文件名**，指定包含存储的过程的 DLL。  
  
4.  有关**程序集名称**，指定程序集的名称。  
  
5.  如果这是一个调试内部版本的库，你将使用调试存储过程中，选择**包含调试信息**复选框。 有关调试存储的过程的详细信息，请参阅[调试存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)。  
  
6.  你可以单击**确定**立即，或在对话框框工具栏上，请注册该程序集，你可以单击命令**脚本**菜单脚本到查询窗口、 文件或剪贴板注册操作。  
  
 注册服务器程序集后，你可以通过右键单击对象资源管理器中的程序集，然后单击配置它**属性**。  
  
## <a name="registering-a-database-assembly-on-the-server"></a>在服务器上注册数据库程序集  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的对象资源管理器中，数据库程序集将列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库下面的“程序集”文件夹中。 数据库程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>在服务器上创建数据库程序集  
  
1.  展开该实例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库在对象资源管理器中，右键单击**程序集**文件夹，，然后单击**新程序集**。 此时将显示**注册数据库程序集**对话框。  
  
2.  有关**类型**指定程序集的类型：  
  
    -   对于托管代码 (CLR) DLL，请指定 .NET 程序集。  
  
    -   对于本机代码 (COM) DLL，请指定 COM DLL。  
  
3.  有关**文件名**，指定包含存储的过程的 DLL。  
  
4.  有关**程序集名称**，指定程序集的名称。  
  
5.  如果这是一个调试内部版本的库，你将使用调试存储过程中，选择**包含调试信息**复选框。 有关调试存储的过程的详细信息，请参阅[调试存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)。  
  
6.  你可以单击**确定**立即，或在对话框框工具栏上，请注册该程序集，你可以单击命令**脚本**菜单脚本到查询窗口、 文件或剪贴板注册操作。  
  
 注册数据库程序集后，你可以通过右键单击对象资源管理器中的程序集，然后单击配置它**属性**。  
  
## <a name="registering-a-database-assembly-in-a-project"></a>在项目中注册数据库程序集  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的解决方案资源管理器中，数据库程序集列在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目下面的“程序集”文件夹中。 数据库程序集可以同时包含 .NET (CLR) 程序集和 COM 库。  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>在 Analysis Service 项目中创建数据库程序集  
  
1.  展开该实例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库在对象资源管理器中，右键单击**程序集**文件夹，，然后单击**新程序集引用**。 此时将显示**添加引用**对话框。 **.NET**选项卡**添加引用**对话框将列出现有的.NET (CLR) 程序集时**项目**选项卡列出项目。  
  
2.  你可以单击某个现有组件或项目，然后单击**添加**将它添加到[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。 若要添加到 COM DLL 的引用，请单击**浏览**选项卡来查找该文件。 **选定的项目和组件**列表显示名称、 类型、 版本和每个组件的要添加到项目的位置。  
  
3.  在完成选择要添加，请单击组件时**确定**将其添加到[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。  
  
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
 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
