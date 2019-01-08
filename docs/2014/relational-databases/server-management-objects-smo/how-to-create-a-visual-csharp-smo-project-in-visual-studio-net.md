---
title: 在 Visual Studio.NET 中创建 Visual C# SMO 项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799494"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>在 Visual Studio .NET 中创建 Visual C# SMO 项目
  本节介绍了如何生成简单的 SMO 控制台应用程序。  
  
 此示例导入命名空间，这样，程序即可以引用 SMO 类型。 可以选择导入 `Agent` 命名空间。 当编写使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的程序时使用此命名空间。 需要使用 `Common` 命名空间来建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的安全连接。 使用 `SqlClient` 命名空间处理 SQL 异常错误。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual studio.net 中创建 Visual C# SMO 项目  
  
1.  启动 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]（或 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]）。  
  
2.  在“文件”菜单中，单击“新建项目”。 此时将显示“新建项目”  对话框。  
  
3.  在中**项目类型**对话框中，选择**Visual C#**，然后选择**Windows**。 在中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]已安装的模板窗格中，选择**Windows 应用程序**。  
  
4.  （可选）在中**名称**字段中，键入新应用程序的名称  
  
5.  选择 Visual C# 应用程序类型。 有关示例，请执行中，选择**控制台应用程序**。  
  
6.  在“项目”菜单中，选择“添加引用”。 此时将显示“添加引用”对话框。  
  
7.  单击**浏览**，找到中的 SMO 程序集[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]文件夹，，然后选择以下文件。 这些文件是构建一个 SMO 应用程序至少需要的文件：  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  使用 `Ctrl` 键可选择多个文件。  
  
8.  添加需要的任何其他 SMO 程序集。 例如，如果您要专门对 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 进行编程，则可以添加以下程序集：  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. 单击 **“打开”**。  
  
10. 上**视图**菜单上，单击**代码**。-或者-选择 Program1.cs [设计] Windows 并双击 windows 窗体以显示代码窗口。  
  
11. 在代码的命名空间语句前，键入以下 `using` 语句，以限定 SMO 命名空间中的类型：  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO 在 Microsoft.SqlServer.Management.Smo 下具有各种命名空间，如 Microsoft.SqlServer.Management.Smo.Agent。 请根据需要添加这些命名空间。  
  
13. 您可以立即添加 SMO 代码。  
  
  
