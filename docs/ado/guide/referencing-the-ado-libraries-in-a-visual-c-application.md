---
title: 引用 ADO 库视觉对象中的C++应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62fb1b89299af1f466e446c8adba422a841f0196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923026"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>在 Visual C++ 应用程序中引用 ADO 库
若要在视觉对象中使用 ADO 的最新版本C++应用程序中，使用以下`#import`指令：  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，必须导入*msadomd.dll*或*msadox.dll*，通过使用上面的语法。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 若要使用任何早期版本的 ADO，替换*msado15.dll*上述其中一个以下类型库。  
  
-   *msado27.tlb*，ADO 2.7 类型库  
  
-   *msado26.tlb*，ADO 2.6 类型库  
  
-   *msado25.tlb*，ADO 2.5 类型库  
  
-   *msado21.tlb*，ADO 2.1 类型库  
  
-   *msado20.tlb*，ADO 2.0 类型库
