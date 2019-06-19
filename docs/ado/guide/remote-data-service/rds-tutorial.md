---
title: RDS 教程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3d1f328baf628e86c75abc9a452600e1f0e8cf88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704256"
---
# <a name="rds-tutorial"></a>RDS 教程
本教程说明了使用 RDS 编程模型来查询和更新数据源。 首先，它介绍了完成此任务所需的步骤。 然后本教程是在 Microsoft® Visual Basic Scripting Edition （特点是 ADO 的 Windows 基础类 (ADO/WFC)） 中重复。  
  
 本教程中是不同的语言编码，原因有两个：  
  
-   RDS 的文档假定在 Visual Basic 中的读取器代码。 这使得文档的 Visual Basic 编程人员带来方便，但不太有用的编程人员使用其他语言。  
  
-   如果你不确定特定的 RDS 功能和有所了解的另一种语言，您可以通过查找在另一种语言中相同的功能来解决您的问题。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="how-the-tutorial-is-presented"></a>本教程的显示方式  
 本教程基于 RDS 编程模型。 它分别讨论每个步骤的编程模型。 此外，它说明了每个步骤的 Visual Basic 代码片段。  
  
 最小讨论其他语言中重复的代码示例。 在给定的编程语言教程中每个步骤的编程模型和描述性教程中标记为与相应的步骤。 使用步骤数来指代描述性本教程中的讨论。  
  
 RDS 编程模型是下一节中所述。 将其用作一个路线图，继续本教程操作。  
  
## <a name="rds-programming-model-with-objects"></a>RDS 编程模型和对象  
  
-   指定的服务器上，要调用的程序并获取方式 （代理） 从客户端引用它。  
  
-   调用服务器程序。 将参数传递给服务器程序，用于标识数据源和要发出的命令。  
  
-   服务器程序获得[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据源，通常通过使用 ADO 对象。 （可选）**记录集**在服务器上处理对象。  
  
-   服务器程序将返回最后一个**记录集**到客户端应用程序对象。  
  
-   在客户端**记录集**（可选） 将对象放入可视控件可以轻松地使用的窗体。  
  
-   将更改为**记录集**发送回发到服务器和用于更新数据源对象。  
  
 本教程包含以下主题。  
  
-   [步骤 1：指定服务器程序 （RDS 教程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [步骤 2：调用服务器程序 （RDS 教程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [步骤 3：服务器获取记录集 （RDS 教程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [步骤 4：服务器返回记录集 （RDS 教程）](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [步骤 5：数据控件不能进行 （RDS 教程）](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [步骤 6：将更改发送到服务器 （RDS 教程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>请参阅  
 [步骤 1：指定服务器程序 （RDS 教程）](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
