---
title: "使用 Microsoft SDK for Java |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e176da2e8f67a61a4f38fa6867919d4c5bfbde7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="using-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java

> [!IMPORTANT]
> Microsoft 在 2004 年 1 月停止使用支持的 Visual J + + 中。

Microsoft SDK for Java 是 Microsoft Internet Explorer 环境的开发人员工具包。 提供工具、 信息和示例来帮助你开发 Java 程序和基于 JDK 1.1 和 Microsoft Win32 虚拟机 （Microsoft 虚拟机） 上的小程序。 Microsoft SDK for Java 未绑定到 Microsoft Visual J + + 中。 若要下载此 SDK，请单击此处。  
  
 该 Jactivex.exe 实用程序从类型库生成的类，但仅在命令行中调用。 此功能未与 Visual J + + 开发环境集成。 与通过 Java 类型库向导生成的类，可以单步执行由 SDK 创建此类包装器。 这可用于调试你的代码如何使用 ADO 包装类。  
  
 此机制读取 ADO 类型库并生成应用程序中可以实例化的类。 在以下位置生成这些类： \\< windows 目录\>\Java\trustlib\msado15。  
  
 在 Java 中使用 Microsoft SDK for Java 创建 ADO 应用程序是完全相同的从代码的源代码，角度来看使用 Java 类型库向导。 有关示例代码，请参阅[ADO Java 类包装](../../../ado/guide/appendixes/ado-java-class-wrappers.md)。 唯一的真正的区别是中如何生成包装类在第一个位置，如以下步骤中所示。  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>使用 Microsoft SDK for Java 中创建的 ADO 项目  
  
1.  在命令提示符处运行以下命令。 必须设置路径以包括 Microsoft SDK for Java 的 Bin 目录中，或从该位置中运行命令。 通常，在与 Visual Studio 相同的位置中安装 Microsoft SDK for Java。 这是单个命令语句。  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  运行以下命令以编译生成的类。 /G: t 开关开启的调试符号的生成，以便能够跟踪到。Java 符号。 为发布版本中删除它。  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  若要使用这些文件，打开你的项目中 Visual J + + 中。 从**项目**菜单上，选择**添加到项目**。 选择**文件**，然后添加的所有。JAVA trustlib\msado15 目录到你的项目中生成文件。  
  
## <a name="see-also"></a>另请参阅  
 [ADO Java 类包装器](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
