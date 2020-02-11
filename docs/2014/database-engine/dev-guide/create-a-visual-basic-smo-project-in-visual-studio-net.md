---
title: 在 Visual Studio .NET 中创建 Visual Basic SMO 项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 662916720b9953e0374bedb29890a36ced0cfac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62753332"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>在 Visual Studio .NET 中创建 Visual Basic SMO 项目
  本节介绍了如何生成简单的 SMO 控制台应用程序。  
  
 此示例导入命名空间，这样，程序即可以引用 SMO 类型。 可以选择导入 `Agent` 命名空间。 当编写使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的程序时使用此命名空间。 需要使用 `Common` 命名空间来建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的安全连接。 使用 `SqlClient` 命名空间处理 SQL 异常错误。  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>在 Visual Studio .NET 中创建 Visual Basic SMO 项目  
  
1.  启动 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]（或 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]）。  
  
2.  在“文件”菜单中，单击“新建项目”。   将显示“新建项目”对话框  。  
  
3.  在 "**项目类型**" 对话框中，选择 " **Visual Basic**"，然后选择 " **Windows**"。 在 " [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]已安装的模板" 窗格中选择 "**控制台应用程序"。**  
  
4.  可有可无在 "**名称**" 字段中，键入新应用程序的名称。  
  
5.  单击 **"确定"** 加载[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] "控制台应用程序" 模板。  
  
6.  在“项目”菜单中，选择“添加引用”。   此时将显示“添加引用”对话框。   
  
7.  单击 "**浏览**"，找到 C:\PROGRAM Files\Microsoft SQL Server\120\SDK\Assemblies 文件夹中的 SMO 程序集，然后选择以下文件。 这些文件是构建一个 SMO 应用程序至少需要的文件：  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  使用 `Ctrl` 键可选择多个文件。  
  
8.  添加需要的任何其他 SMO 程序集。 例如，如果您要专门对 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 进行编程，则可以添加以下程序集：  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. 单击 **“打开”** 。  
  
10. 在 "**视图**" 菜单上，单击 "**代码**"，或选择 "Module1" 窗口以显示代码窗口。  
  
11. 在代码的任何声明前，键入以下**Imports**语句以限定 SMO 命名空间中的类型。  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO 在 Microsoft.SqlServer.Management.Smo 下具有各种命名空间，如 Microsoft.SqlServer.Management.Smo.Agent。 请根据需要添加这些命名空间。  
  
13. 您可以立即添加 SMO 代码。  
  
  
