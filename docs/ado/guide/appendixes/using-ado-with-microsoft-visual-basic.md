---
title: "使用与 Microsoft Visual Basic 的 ADO |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c88dbb57318fe960eab28c463b8c46a5546ffd5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>使用 ADO 使用 Microsoft Visual Basic 和 Visual Basic for Applications
设置 ADO 项目并编写 ADO 代码非常类似是否为应用程序使用 Visual Basic 或 Visual Basic。 本主题介绍使用 Visual Basic 和 Visual Basic 中为应用程序使用 ADO，并且说明的任何差异。

## <a name="referencing-the-ado-library"></a>引用 ADO 库
 ADO 库必须由你的项目引用。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>若要引用从 Microsoft Visual Basic 的 ADO

1.  在 Visual Basic 中，从**项目**菜单上，选择**引用...**.

2.  选择**Microsoft ActiveX 数据对象 x.x 库**从列表中。 验证至少还会选择以下库：

    -   Visual Basic for Applications

    -   Visual Basic 运行时对象和过程

    -   Visual Basic 对象和过程

    -   OLE 自动化

3.  单击 **“确定”**。

 你可以使用 ADO 轻松地使用 Visual Basic 应用程序，例如通过使用 Microsoft Access。

#### <a name="to-reference-ado-from-microsoft-access"></a>若要从 Microsoft Access 引用 ADO

1.  在 Microsoft Access 中，选择或创建的模块**模块**选项卡中**数据库**窗口。

2.  上**工具**菜单上，选择**引用...**.

3.  选择**Microsoft ActiveX 数据对象 x.x 库**从列表中。 验证至少还会选择以下库：

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 对象库 （或更高版本）

    -   Microsoft DAO 3.5 对象库 （或更高版本）

4.  单击 **“确定”**。

## <a name="creating-ado-objects-in-visual-basic"></a>在 Visual Basic 中创建 ADO 对象
 若要创建一个自动化变量，并为该变量的对象的实例，可以使用两种方法： **Dim**或**CreateObject**。

### <a name="dim"></a>Dim
 你可以使用**新建**关键字后的跟**Dim**声明并在一个步骤中创建的 ADO 对象的实例：

```
Dim conn As New ADODB.Connection
```

 或者， **Dim**语句声明和对象实例化也可以是两个步骤：

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  它不需要显式使用`ADODB`progid 与**Dim**语句，假定你正确引用 ADO 库项目中。 但是，使用它可确保，你将不具有与其他库发生命名冲突。

> [!NOTE]
>  例如，如果你在同一项目包含对 ADO 和 DAO 的引用，则应包含限定符来指定要在实例化时使用的对象模型**记录集**对象，如以下代码所示：

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 与**CreateObject**方法、 声明和对象实例化必须是两个独立的步骤：

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 对象实例化的**CreateObject**是后期绑定，这意味着，它们不强类型和命令行完成下为禁用。 但是，它允许你可以跳过从你的项目，引用 ADO 库，并使你能够实例化的对象的特定版本。 例如：

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 你也无法通过专门创建对 ADO 版本 2.0 类型库的引用并创建对象完成此操作。

 使用实例化对象**CreateObject**方法速度通常比使用较慢**Dim**语句。

## <a name="handling-events"></a>处理事件
 若要处理 ADO 事件在 Microsoft Visual Basic 中，您必须声明模块级变量 using **WithEvents**关键字。 变量可以声明仅为类模块的一部分，并且必须在模块级别声明。 有关处理 ADO 事件的更详细的讨论，请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。

## <a name="visual-basic-examples"></a>Visual Basic 示例
 ADO 文档中附带了许多 Visual Basic 示例。 有关详细信息，请参阅[ADO 代码示例在 Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)。

## <a name="see-also"></a>另请参阅
 [Microsoft ActiveX 数据对象 (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [中使用 ADO 的 Microsoft Visual c + +](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [中使用 ADO 的脚本语言](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

