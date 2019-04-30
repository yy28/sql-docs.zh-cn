---
title: 引用 ADO 库在 Visual Basic 6 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8e37459c5e48fe817a3bdbb6a824550cf977f66
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222035"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>在 Visual Basic 6 应用程序中引用 ADO 库
要导入到 Microsoft Visual Basic 6 应用程序中的 ADO 库，必须在 Visual Basic 项目中设置的引用。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>若要在 Visual Basic 项目中设置的引用 ADO 库  
  
1.  创建新的或打开现有的 Visual Basic 项目。  
  
2.  单击**项目**菜单项并选择**引用...** 下拉列表菜单面板中。  
  
3.  从**可用的引用**，选中的复选框**Microsoft ActiveX 数据对象*n.n*库**，其中***n.n***表示最新版本号。 **位置**下面的字段应确定为所选 *$installDir\msado15.dll*，其中 *$installDir*表示在其中的目录的路径的 ADO 库已安装。  
  
4.  如果你想要使用 ADO MD，重复步骤 3 以选择**Microsoft ActiveX 数据对象 （多维） *n.n*库**。 **位置**字段应确定此选项作为 *$installDir\msadomd.dll*。  
  
5.  如果你想要使用 ADOX，重复步骤 3 以选择**Microsoft ADO ext. *n.n* DDL 和安全**。 **位置**字段应确定此选项作为 *$installDir\msadox.dll*。  
  
6.  单击**确定**完成设置引用。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 安装 ADO 还将复制早期版本的以下类型的库：  
  
-   *msado27.tlb*，ADO 2.7 类型库  
  
-   *msado26.tlb*，ADO 2.6 类型库  
  
-   *msado25.tlb*，ADO 2.5 类型库  
  
-   *msado21.tlb*，ADO 2.1 类型库  
  
-   *msado20.tlb*，ADO 2.0 类型库  
  
 如果你的应用程序必须使用其中任何 ADO 库出于向后兼容性，需要导入类型库的适当版本。 若要执行此操作，请按照上一节中的过程替换*msado15.dll*通过*msadoXX.tlb*，其中*XX*表示需要导入的版本号。
