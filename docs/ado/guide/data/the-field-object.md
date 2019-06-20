---
title: 字段对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a709b8c26c3cdee3a6087444e4acebbd212caf66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718661"
---
# <a name="the-field-object"></a>字段对象
每个**字段**对象通常对应于数据库表中的列。 但是，**字段**还表示到另一个指针**记录集**，名为一章。 将在本指南的后面介绍异常，如章节列。  
  
 使用**值**的属性**字段**对象设置或返回当前记录的数据。 根据的功能提供程序用于公开，一些集合、 方法或属性的**字段**对象可能不可用。  
  
 使用集合、 方法和属性的**字段**对象，您可以执行以下操作：  
  
-   通过使用返回的字段名称**名称**属性。  
  
-   查看或更改字段中的数据通过使用**值**属性。 **值**是默认属性**字段**对象。  
  
-   通过使用返回的字段的基本特征**类型**，**精度**，并**NumericScale**属性。  
  
-   通过使用返回的字段声明的大小**DefinedSize**属性。  
  
-   使用给定字段中返回数据的实际大小**ActualSize**属性。  
  
-   确定给定字段的使用支持哪些类型的功能**特性**属性和**属性**集合。  
  
-   操作通过使用包含长度的二进制或长字符数据字段的值**AppendChunk**并**GetChunk**方法。  
  
 解决使用批更新过程中的字段值中的差异**OriginalValue**并**UnderlyingValue**属性，如果提供程序支持批更新。  
  
## <a name="describing-a-field"></a>描述字段  
 按照将的主题讨论的属性[字段](../../../ado/reference/ado-api/field-object.md)对象，它表示描述的信息**字段**对象本身-即，有关该字段的元数据。 此信息可以用于确定许多有关的架构**记录集**。 这些属性包括**类型**， **DefinedSize**并**ActualSize**，**名称**，和**NumericScale**并**精度**。  
  
### <a name="discovering-the-data-type"></a>发现的数据类型  
 **类型**属性指示该字段的数据类型。 中介绍了支持的 ADO 枚举的常量的数据类型[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)中*ADO 程序员参考*。  
  
 为浮点型数值类型等**adNumeric**，可以获取详细信息。 **NumericScale**属性指示用于代表的值小数点右侧的位数**字段**。 **精度**属性指定用于表示值的最大位数**字段**。  
  
### <a name="determining-field-size"></a>确定字段大小  
 使用**DefinedSize**属性来确定的数据容量**字段**对象。  
  
 使用**ActualSize**属性返回的实际长度**字段**对象的值。 为所有字段**ActualSize**属性是只读的。 如果 ADO 无法确定的长度**字段**对象的值**ActualSize**属性返回**adUnknown**。  
  
 **DefinedSize**并**ActualSize**属性具有不同的用途。 例如，考虑**字段**对象的声明的类型**adVarChar**和一个**DefinedSize**属性值为 50，包含单个字符。 **ActualSize**它将返回的属性值是单个字符的长度以字节为单位。  
  
### <a name="determining-field-contents"></a>确定字段内容  
 表示数据源的列的标识符**名称**的属性**字段**。 **值**的属性**字段**对象返回或设置字段的实际数据内容。 这是默认属性。  
  
 若要更改一个字段中的数据，请设置**值**属性等于正确类型的新值。 游标类型必须支持更新，才能更改字段的内容。 数据库验证不是此处在批处理模式下，因此将需要检查是否有错误时调用**UpdateBatch**这种情况。 某些提供程序还支持 ADO**字段**对象的**UnderlyingValue**并**OriginalValue**属性可帮助您进行时尝试解决冲突执行批处理更新。 有关如何解决此类冲突的详细信息，请参阅[编辑数据](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  **记录集字段**值不能设置新追加**字段**到**记录集**。 相反，新**字段**可将其附加到已关闭**记录集**。 然后**记录集**必须是已打开，并仅然后可以将值分配给这些**字段**。  
  
### <a name="getting-more-field-information"></a>获取字段的详细信息  
 ADO 对象具有两种类型的属性： 内置和动态。 到目前为止的内置属性仅**字段**讨论了对象。  
  
 内置属性是这些属性在 ADO 中实现，并立即可用于任何新对象，请使用`MyObject.Property`语法。 它们不显示为**属性**对象中的对象**属性**集合。  
  
 动态属性定义的基础数据提供程序，并且显示在**属性**为适当的 ADO 对象的集合。 例如，可能表示特定于提供程序的属性，如果**记录集**对象支持的事务或更新。 这些附加属性将显示为**属性**对象中的**记录集**对象的**属性**集合。 动态属性可以引用仅遍历该集合，使用语法`MyObject.Properties(0)`或`MyObject.Properties("Name")`。  
  
 不能删除这两种属性。  
  
 动态**属性**对象都有其自己的四个内置属性：  
  
-   **名称**属性是一个字符串，标识的属性。  
  
-   **类型**属性是一个整数，指定属性数据类型。  
  
-   **值**属性是变体，其中包含属性设置。 **值**是默认属性**属性**对象。  
  
-   **特性**属性是**长**值，该值指示属性特定于提供程序的特征。  
  
 **属性**集合**字段**对象包含有关字段的其他元数据。 此集合的内容因提供程序而异。 下面的代码示例将检查**属性**的示例集合**记录集**引入了在本部分的开头。 它首先会查看集合的内容。 此代码使用[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此**属性**集合包含与该提供程序相关的信息。  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>处理二进制数据  
 使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法**字段**要用长二进制或字符数据填充对象。 在系统内存有限的情况下，你可以使用**AppendChunk**方法来操作部分而不是很长的值。  
  
 如果**adFldLong**位**特性**属性**字段**对象设置为**True**，可以使用**AppendChunk**为该字段的方法。  
  
 第一个**AppendChunk**上调用**字段**对象将数据写入到字段中，覆盖任何现有数据。 后续**AppendChunk**调用添加到现有数据。 如果将数据追加到的一个字段，然后设置或读取的当前记录中的另一个字段的值，ADO 将假定您已完成了将数据追加到第一个字段。 如果您调用**AppendChunk**同样，第一个字段 ADO 方法将解释为一个新的调用**AppendChunk**操作，并覆盖现有数据。 访问其他字段**记录集**不是第一个克隆的对象**记录集**对象不会破坏**AppendChunk**操作。  
  
 使用**GetChunk**方法**字段**要检索其长二进制或字符数据的部分或全部对象。 在系统内存有限的情况下，你可以使用**GetChunk**方法来操作部分，而不是很长的值。  
  
 数据的**GetChunk**调用返回分配给*变量*。 如果*大小*大于剩余数据**GetChunk**方法仅返回的其余数据而无需填充*变量*具有空白空间。 如果该字段为空， **GetChunk**方法将返回 null 值。  
  
 每个后续**GetChunk**调用会检索数据从何处开始以前**GetChunk**离开的调用。 但是，如果从一个字段中检索数据和设置或读取的当前记录中的另一个字段的值，ADO 假定你已完成从第一个字段中检索数据。 如果您调用**GetChunk**同样，第一个字段 ADO 方法将解释为一个新的调用**GetChunk**操作并开始读取数据的起始位置。 访问其他字段**记录集**不是第一个克隆的对象**记录集**对象不会破坏**GetChunk**操作。  
  
 如果**adFldLong**位**特性**属性**字段**对象设置为**True**，可以使用**GetChunk**为该字段的方法。  
  
 如果没有最新记录时使用**GetChunk**或**AppendChunk**方法**字段**对象时，会发生错误 3021 （最新记录）。  
  
 有关使用这些方法来处理二进制数据的示例，请参阅[AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)并[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)中的示例*ADO 程序员参考*。
