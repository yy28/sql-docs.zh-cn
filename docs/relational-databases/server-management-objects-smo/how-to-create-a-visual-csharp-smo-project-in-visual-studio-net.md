---
title: 在 Visual Studio.NET 中创建 Visual C# SMO 项目 |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2bc775f7f857bffb5a7840d99de00fc546e71d03
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717985"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>如何在 Visual Studio .NET 中创建 Visual C# SMO 项目
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  本节介绍了如何生成简单的 SMO 控制台应用程序。  
  
 此示例导入命名空间，这样，程序即可以引用 SMO 类型。 在导入**代理**是可选的命名空间。 当编写使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的程序时使用此命名空间。 **常见**建立安全连接到的实例所需的命名空间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **SqlClient**命名空间用于处理 SQL 异常错误。  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>在 Visual studio.net 中创建 Visual C# SMO 项目  
  
1. 启动 Visual Studio
  
2. 上**文件**菜单上，单击**新建**，然后**项目**。  此时将显示“新建项目”  对话框。   
  
3. 在中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]**已安装**窗格中，导航到**模板**\\**Visual C#**\\**Windows**然后选择**控制台应用程序**。  
  
4. （可选）在中**名称**文字框中，键入新应用程序的名称。  

5. 单击**确定**加载控制台应用程序模板。  

6. 按照上的说明[安装 SMO](installing-smo.md)安装项目来引用的包。
  
7. 在 **“视图”** 菜单上，单击 **“代码”**。
    
8. 在代码中，命名空间语句前，键入以下内容**使用**语句以限定 SMO 命名空间中的类型：
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO 在 Microsoft.SqlServer.Management.Smo 下具有各种命名空间，如 Microsoft.SqlServer.Management.Smo.Agent。 请根据需要添加这些命名空间。  
  
16. 您可以立即添加 SMO 代码。  
  
  
