---
title: "引用在 Visual Basic 6 应用程序的 ADO 库 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 937934fd297c876fa023ddae89ac027068bb20c9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>引用在 Visual Basic 6 应用程序的 ADO 库
若要将 ADO 库导入一个 Microsoft Visual Basic 6 应用程序，必须在 Visual Basic 项目中设置的引用。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>在 Visual Basic 项目中设置对 ADO 库的引用  
  
1.  创建一个新或打开现有的 Visual Basic 项目。  
  
2.  单击**项目**菜单项，然后选择**引用...**从下拉列表菜单面板。  
  
3.  从**可用引用**，选中对应的框**Microsoft ActiveX 数据对象*n.n*库**，其中***n.n***表示最新版本号。 **位置**下面字段应标识为所选*$installDir\msado15.dll*，其中*$installDir*表示在其中的目录的路径的 ADO 库已安装。  
  
4.  如果你想要使用 ADO MD，重复步骤 3 以选择**Microsoft ActiveX 数据对象 （多维） *n.n*库**。 **位置**字段应标识作为此选择*$installDir\msadomd.dll*。  
  
5.  如果你想要使用 ADOX，重复步骤 3 以选择**Microsoft ADO 分机*n.n* DDL 和安全**。 **位置**字段应标识作为此选择*$installDir\msadox.dll*。  
  
6.  单击**确定**完成设置引用。  
  
## <a name="backward-compatibility"></a>向后兼容性  
 安装 ADO 还会将复制早期版本的以下类型的库：  
  
-   *msado27.tlb*，ADO 2.7 类型库  
  
-   *msado26.tlb*，ADO 2.6 类型库  
  
-   *msado25.tlb*，ADO 2.5 类型库  
  
-   *msado21.tlb*，ADO 2.1 类型库  
  
-   *msado20.tlb*，ADO 2.0 类型库  
  
 如果你的应用程序必须使用任何这些 ADO 库的向后兼容性原因，你需要导入类型库的适当版本。 若要执行此操作，请按照上一节中的过程替换*msado15.dll*通过*msadoXX.tlb*，其中*XX*表示需要导入的版本号。
