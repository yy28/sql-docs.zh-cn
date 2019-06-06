---
title: 使用 Microsoft SDK for Java |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 84c342150d00c399c4ab41c20d513b84f7be36db
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701161"
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Java 适用的 Microsoft SDK

> [!IMPORTANT]
> Microsoft 不再支持的 Visual J + + 中使用在 2004 年 1 月。

Microsoft SDK for Java 是适用于 Microsoft Internet Explorer 环境的开发人员工具包。 提供工具、 信息和示例来帮助您开发 Java 程序和基于 JDK 1.1 和 Microsoft Win32 虚拟机 (Microsoft VM) 上的小程序。 Microsoft SDK for Java 不被绑定到 Microsoft Visual J + +。 若要下载此 SDK，请单击此处。  
  
 Jactivex.exe 实用程序从类型库生成类，但只能在命令行上调用。 此功能不与 Visual J + + 开发环境集成。 与不同的是由 Java 类型库向导生成的类，可以单步执行由 SDK 所创建的类包装。 这是用于调试你的代码如何使用 ADO 的包装类。  
  
 此机制读取 ADO 类型库并生成可以在应用程序中实例化的类。 在以下位置生成这些类： \\< windows 目录\>\Java\trustlib\msado15。  
  
 在 Java 中使用 Microsoft SDK for Java 创建 ADO 应用程序是从根本上说完全相同，从源代码的角度来看使用 Java 类型库向导。 有关示例代码，请参阅[ADO Java 类包装器](../../../ado/guide/appendixes/ado-java-class-wrappers.md)。 唯一的真正差别是如何生成包装类首先，如以下步骤中所示。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>若要使用 Microsoft SDK for Java 创建一个 ADO 项目  
  
1.  在命令提示符处运行以下命令。 必须设置要包括 Microsoft SDK for Java 的 Bin 目录的路径，或从该位置运行该命令。 通常，Microsoft SDK for Java 安装在与 Visual Studio 相同的位置。 这是单个命令语句。  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  运行以下命令以编译生成的类。 /G: t 开关启用生成的调试符号，以便可以跟踪到。Java 符号。 用于发布版本中删除它。  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用这些文件，打开你的项目中 Visual J + +。 从**项目**菜单中，选择**添加到项目**。 选择**文件**，然后添加的所有。JAVA trustlib\msado15 目录到你的项目中生成文件。  
  
## <a name="see-also"></a>请参阅  
 [ADO Java 类包装器](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
