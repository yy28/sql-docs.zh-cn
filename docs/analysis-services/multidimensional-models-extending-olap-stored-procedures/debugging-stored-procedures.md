---
title: "调试存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b605ee9a2af577048c03d406ff628b1d279a68e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="debugging-stored-procedures"></a>调试存储的过程
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  实际上，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储过程是使用 C#（或任何其他 CLR 或 COM 语言）编写的 CLR 或 COM 库（通常为 DLL）。 因此，调试存储过程类似于在 Visual Studio 调试环境中调试任何其他应用程序。 您可以使用集成调试功能在 Visual Studio 开发环境中调试存储过程。 您可以使用这些功能执行下列操作：在过程位置停止、检查内存和注册值、更改变量、观察消息流量以及密切监视代码的运行状况。  
  
### <a name="to-debug-a-stored-procedure"></a>调试存储过程  
  
1.  在 Visual Studio 中打开用于创建 DLL 的项目。  
  
2.  使用要调试的过程相应的方法或函数创建断点。  
  
3.  使用 Visual Studio 创建存储过程 DLL 的调试版本。  
  
4.  将 DLL 部署到服务器中。 有关将 DLL 部署到服务器的详细信息，请参阅[创建存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)。  
  
5.  您需要一个调用要进行测试的存储过程的应用程序。 如果没有此类可用的应用程序，则可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 MDX 查询编辑器创建调用要进行测试的存储过程的 MDX 查询。  
  
6.  在 Visual Studio 中，附加到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进程 (Msmdsrv.exe)。  
  
    1.  从**调试**菜单上，选择**Attatch toProcess**。  
  
    2.  在**Attatch toProcess**对话框中，选择**显示来自所有用户的进程**。  
  
    3.  在**可用进程**列表中，**过程**列中，单击**Msmdsrv.exe**。 如果服务器上运行多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，则需要通过要使用的实例的 ID 标识进程。  
  
    4.  在**将附加到**文本框中，请确保选择相应的程序类型。 有关 CLR DLL，请单击**选择**，然后单击**调试以下代码类型**，然后单击**托管**，然后单击**确定**。 COM DLL，请单击**选择**，然后单击**调试以下代码类型**，然后单击**本机**，然后单击**确定**。  
  
    5.  单击**附加**。  
  
7.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，调用程序或 MDX 脚本（用于调用存储过程）。 当调试程序到达包含断点的某行时，便会中断。 您可以在监视窗口中计算变量，查看局部变量并逐句检查代码。  
  
 如果在调试库时出现问题，则确保已将对应的程序数据库 (PDB) 文件复制到服务器中的部署位置。 如果在注册或部署过程中没有复制该文件，则必须手动将其复制到 DLL 所在的位置。 对于本机代码 (COM DLL)，PDB 文件驻留在 \debug 子目录中。 对于托管代码 (CLR DLL)，该文件驻留在 \WINDEBUG 子目录中。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储的过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
