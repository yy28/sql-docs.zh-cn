---
title: 使用 ADO 与 Microsoft Visual Basic |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d409f874e9fcec059c01ddef91d83d8a70fdeb47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864513"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>使用 ADO 与 Microsoft Visual Basic 和 Visual Basic for Applications
设置 ADO 项目并编写的 ADO 代码非常类似是否为应用程序使用 Visual Basic 或 Visual Basic。 本主题介绍使用 Visual Basic 和 Visual Basic 中为应用程序使用 ADO，并且说明任何差异。

## <a name="referencing-the-ado-library"></a>引用 ADO 库
 你的项目必须引用 ADO 库。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>若要从 Microsoft Visual Basic 引用 ADO

1.  在 Visual Basic 中，从**项目**菜单中，选择**引用...**.

2.  选择**Microsoft ActiveX 数据对象 x.x 库**从列表中。 验证至少也选中以下库：

    -   Visual Basic for Applications

    -   Visual Basic 运行时对象和过程

    -   Visual Basic 对象和过程

    -   OLE 自动化

3.  单击“确定” 。

 您可以使用 ADO 轻松地使用 Visual Basic 应用程序，通过使用 Microsoft Access 中，例如。

#### <a name="to-reference-ado-from-microsoft-access"></a>若要从 Microsoft Access 中引用 ADO

1.  在 Microsoft Access 中，选择或创建从一个模块**模块**选项卡**数据库**窗口。

2.  上**工具**菜单中，选择**引用...**.

3.  选择**Microsoft ActiveX 数据对象 x.x 库**从列表中。 验证至少也选中以下库：

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 对象库 （或更高版本）

    -   Microsoft DAO 3.5 对象库 （或更高版本）

4.  单击“确定” 。

## <a name="creating-ado-objects-in-visual-basic"></a>Visual Basic 中创建 ADO 对象
 若要创建一个自动化变量，并为该变量的对象的实例，可以使用两个方法：**Dim**或**CreateObject**。

### <a name="dim"></a>Dim
 可以使用**新建**关键字**Dim**声明并在一个步骤中创建的 ADO 对象的实例：

```
Dim conn As New ADODB.Connection
```

 或者， **Dim**语句声明和对象实例化也可以是两个步骤：

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  它不需要显式使用`ADODB`与 progid **Dim**语句中，假设已正确在项目中引用 ADO 库。 但是，使用它可确保你将具有命名冲突与其他库。

> [!NOTE]
>  例如，如果在同一项目中包括对 ADO 和 DAO 的引用，应包含以指定要实例化时使用的对象模型的限定符**记录集**对象，如以下代码所示：

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 与**CreateObject**方法、 声明和对象实例化必须是两个不连续的步骤：

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 使用对象实例化**CreateObject**是后期绑定的这意味着，它们不强类型和命令行完成已禁用。 但是，它允许您跳过从你的项目，引用 ADO 库并使你能够实例化对象的特定版本。 例如：

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 您还可以通过专门创建对 ADO 版本 2.0 类型库的引用并创建对象完成此操作。

 通过实例化对象**CreateObject**方法是使用比通常慢**Dim**语句。

## <a name="handling-events"></a>处理事件
 若要处理 ADO 事件在 Microsoft Visual Basic 中，您必须声明模块级变量 using **WithEvents**关键字。 变量可以声明仅为类模块的一部分，且必须在模块级别声明。 处理 ADO 事件的更深入讨论，请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。

## <a name="visual-basic-examples"></a>Visual Basic 示例
 使用 ADO 文档中包含很多 Visual Basic 示例。 有关详细信息，请参阅[Microsoft Visual Basic 中的 ADO 代码示例](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)。

## <a name="see-also"></a>请参阅
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [配合使用 ADO 与 Microsoft Visual C++ ](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [配合使用 ADO 与脚本语言](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
