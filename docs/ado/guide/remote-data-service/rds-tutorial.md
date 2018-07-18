---
title: RDS 教程 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dca0329dc201d50335983c9078f85e31f8302d0d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274246"
---
# <a name="rds-tutorial"></a>RDS 教程
本教程演示如何使用 RDS 编程模型来查询和更新数据源。 首先，它描述完成此任务所需的步骤。 然后在 Microsoft® Visual Basic Scripting Edition （采用 ADO 的 Windows 基础类 (ADO/WFC)） 重复本教程。  
  
 原因有两个情况下，本教程编码以不同的语言：  
  
-   RDS 的文档假定在 Visual Basic 中的读取器代码。 这使文档方便 Visual Basic 程序员提供的但区别用处不大的程序员来说使用其他语言。  
  
-   如果你不确定特定的 RDS 功能并且您知道有点的另一种语言，你可能能够通过查找其他语言相同的功能来解决你的问题。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="how-the-tutorial-is-presented"></a>本教程中的显示方式  
 本教程基于 RDS 编程模型。 它单独讨论的编程模型的每个步骤。 此外，它说明了每个步骤的 Visual Basic 代码片段。  
  
 在很少进行讨论与其他语言中重复的代码示例。 给定的编程语言教程中的每个步骤的编程模型和描述性教程在标记为与相应的步骤。 使用步骤的数来指代描述性教程中的描述。  
  
 RDS 编程模型是下一节中所述。 使用它作为路线图继续执行本教程。  
  
## <a name="rds-programming-model-with-objects"></a>RDS 的编程模型和对象  
  
-   指定要在服务器上，调用的程序，并获取的方法 （代理） 来引用它从客户端。  
  
-   调用服务器程序。 将参数传递给服务器计划，用于标识数据源和要发出的命令。  
  
-   服务器计划获取[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据源，通常通过使用 ADO 的对象。 （可选）**记录集**在服务器上处理对象。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序对象。  
  
-   在客户端，**记录集**对象 （可选） 放到可以轻松地使用由 visual 控件的窗体。  
  
-   更改为**记录集**发送回发到服务器和用于更新数据源对象。  
  
 本教程包含以下主题。  
  
-   [步骤 1：指定服务器程序（RDS 教程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步骤 2：调用服务器程序（RDS 教程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步骤 3：服务器获取记录集（RDS 教程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步骤 4：服务器返回记录集（RDS 教程）](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步骤 5：DataControl 变为可用（RDS 教程）](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步骤 6：将更改发送到服务器（RDS 教程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>请参阅  
 [步骤 1： 指定的服务器程序 （RDS 教程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
