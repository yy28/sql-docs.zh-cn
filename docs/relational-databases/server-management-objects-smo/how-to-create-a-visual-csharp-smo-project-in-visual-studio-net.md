---
title: 在 Visual Studio C# .net 中创建 Visual SMO 项目 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3989c49d800a9f485c8562aed4406c57216eed77
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909800"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何在 Visual Studio .NET 中创建 Visual C# SMO 项目
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本节介绍了如何生成简单的 SMO 控制台应用程序。  
  
 此示例导入命名空间，这样，程序即可以引用 SMO 类型。 **代理**命名空间的导入是可选的。 当编写使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的程序时使用此命名空间。 需要**公共**命名空间才能建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安全连接。 **SqlClient**命名空间用于处理 SQL 异常错误。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual Studio.NET C#中创建 visual SMO 项目  
  
1. 启动 Visual Studio
  
2. 在 "**文件**" 菜单上，单击 "**新建**"，然后单击 "**项目**"。  此时将显示“新建项目” 对话框。   
  
3. 在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**安装**"窗格中，导航到" **\\C# Visual**\\**Windows**的**模板**"，然后选择"**控制台应用程序**"。  
  
4. 可有可无在 "**名称**" 文本框中，键入新应用程序的名称。  

5. 单击 **"确定"** 加载 "控制台应用程序" 模板。  

6. 按照[安装 SMO](installing-smo.md)上的说明安装要引用的项目包。
  
7. 在 **“视图”** 菜单上，单击 **“代码”** 。
    
8. 在代码的命名空间语句前，键入以下**using**语句以限定 SMO 命名空间中的类型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 下具有各种命名空间，如 Microsoft.SqlServer.Management.Smo.Agent。 请根据需要添加这些命名空间。  
  
16. 您可以立即添加 SMO 代码。  

