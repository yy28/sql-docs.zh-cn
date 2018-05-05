---
title: 在 Visual Studio.NET 中创建 Visual C# SMO 项目 |Microsoft 文档
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 25e06aa3493b10e5a282fc5a709605eae18cb5fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何在 Visual Studio.NET 中创建 Visual C# SMO 项目
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本节介绍了如何生成简单的 SMO 控制台应用程序。  
  
 此示例导入命名空间，这样，程序即可以引用 SMO 类型。 在导入**代理**是可选的命名空间。 当编写使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的程序时使用此命名空间。 **常见**建立安全连接到的实例所需的命名空间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **SqlClient**命名空间用于处理 SQL 异常错误。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio.NET 中创建 Visual C# SMO 项目  
  
1. 启动 Visual Studio
  
2. 上**文件**菜单上，单击**新建**然后**项目**。  此时将显示“新建项目”  对话框。   
  
3. 在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**已安装**窗格中，导航到**模板**\\**Visual C#**\\**Windows**然后选择**控制台应用程序**。  
  
4. （可选）在**名称**文本框中，键入新的应用程序的名称。  

5. 单击**确定**来加载控制台应用程序模板。  

6. 按照上的说明[安装 SMO](installing-smo.md)安装项目，以引用的包。
  
7. 在 **“视图”** 菜单上，单击 **“代码”**。
    
8. 在代码中之前的命名空间语句中，, 键入以下命令**使用**语句来限定 SMO 命名空间中的类型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 下具有各种命名空间，如 Microsoft.SqlServer.Management.Smo.Agent。 请根据需要添加这些命名空间。  
  
16. 您可以立即添加 SMO 代码。  
  
  
