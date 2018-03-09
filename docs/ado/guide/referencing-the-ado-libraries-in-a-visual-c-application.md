---
title: "引用在 Visual c + + 应用程序中的 ADO 库 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a554ff290c1ea3fa8ef5382e45fafbae5b1110d8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>引用在 Visual c + + 应用程序中的 ADO 库
若要使用 ADO 的 Visual c + + 应用程序中的最新版本，请使用以下`#import`指令：  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 若要使用 ADO MD 或 ADOX，必须导入*msadomd.dll*或*msadox.dll*，通过使用上面的语法。  
  
## <a name="backward-compatibility"></a>向后兼容性  
 若要使用任何早期版本的 ADO，替换*msado15.dll*上面使用的以下类型库之一。  
  
-   *msado27.tlb*，ADO 2.7 类型库  
  
-   *msado26.tlb*，ADO 2.6 类型库  
  
-   *msado25.tlb*，ADO 2.5 类型库  
  
-   *msado21.tlb*，ADO 2.1 类型库  
  
-   *msado20.tlb*，ADO 2.0 类型库
