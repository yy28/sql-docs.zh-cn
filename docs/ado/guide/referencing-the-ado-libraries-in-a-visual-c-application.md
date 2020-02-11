---
title: 在 Visual C++ 应用程序中引用 ADO 库 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923026"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>在 Visual C++ 应用程序中引用 ADO 库
若要在 Visual C++ 应用程序中使用最新版本的 ADO，请`#import`使用以下指令：  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，必须使用上述语法导入*msadomd*或*msadox。*  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 若要使用 ADO 的任何早期版本，请将上面的*msado15.dll*替换为以下类型库之一。  
  
-   *msado27*，ADO 2.7 类型库  
  
-   *msado26*，ADO 2.6 类型库  
  
-   *msado25*，ADO 2.5 类型库  
  
-   *msado21*，ADO 2.1 类型库  
  
-   *msado20*，ADO 2.0 类型库
