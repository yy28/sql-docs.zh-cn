---
title: "字段对象 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ecd2382d15536a5c2ebd2b2098c89c41c78ba1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="the-field-object"></a>字段对象
每个**字段**对象通常对应于数据库表中的列。 但是，**字段**还可以表示指针到另一个**记录集**，调用一章。 异常，如章节列，将在本指南后面进行介绍。  
  
 使用**值**属性**字段**对象设置或返回当前记录的数据。 根据的功能提供程序的公开，一些集合、 方法或属性的**字段**对象可能不可用。  
  
 使用集合、 方法和属性的**字段**对象，你可以执行以下操作：  
  
-   使用返回的字段名称**名称**属性。  
  
-   查看或更改字段中的数据使用**值**属性。 **值**是默认属性**字段**对象。  
  
-   使用返回的字段的基本特征**类型**，**精度**，和**NumericScale**属性。  
  
-   使用返回的字段声明的大小**DefinedSize**属性。  
  
-   使用给定字段中返回数据的实际大小**ActualSize**属性。  
  
-   确定哪些类型的功能为给定字段支持使用**属性**属性和**属性**集合。  
  
-   操作通过使用包含长度的二进制或长时间字符数据字段的值**AppendChunk**和**GetChunk**方法。  
  
 在批更新通过使用期间解决字段值中的差异**OriginalValue**和**UnderlyingValue**属性，如果该提供程序支持批量更新。  
  
## <a name="describing-a-field"></a>描述字段  
 请按照将的主题讨论的属性[字段](../../../ado/reference/ado-api/field-object.md)表示描述的信息的对象**字段**对象本身-即，有关该字段的元数据。 此信息可以用于确定有关的架构的很多**记录集**。 这些属性包括**类型**， **DefinedSize**和**ActualSize**，**名称**，和**NumericScale**和**精度**。  
  
### <a name="discovering-the-data-type"></a>发现的数据类型  
 **类型**属性指示的字段的数据类型。 中描述了支持的 ADO 的枚举的常数的数据类型[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)中*ADO 程序员参考*。  
  
 为浮点数字类型如**adNumeric**，你可以获取详细信息。 **NumericScale**属性指示将使用多少小数点右侧的位数来表示值**字段**。 **精度**属性指定用于表示值的数字的最大数**字段**。  
  
### <a name="determining-field-size"></a>确定字段大小  
 使用**DefinedSize**属性来确定的数据容量**字段**对象。  
  
 使用**ActualSize**属性返回的实际长度**字段**对象的值。 为所有字段， **ActualSize**属性是只读的。 如果 ADO 无法确定的长度**字段**对象的值， **ActualSize**属性返回**adUnknown**。  
  
 **DefinedSize**和**ActualSize**属性具有不同的用途。 例如，考虑**字段**的声明的类型的对象**以便您可以排除**和**DefinedSize**属性值为 50，包含单个字符。 **ActualSize**它将返回的属性值是单个字符的长度以字节为单位。  
  
### <a name="determining-field-contents"></a>确定字段内容  
 数据源的列的标识符都由**名称**属性**字段**。 **值**属性**字段**对象返回或设置字段的实际数据内容。 这是默认属性。  
  
 若要更改字段中的数据，设置**值**属性等于正确类型的新值。 游标类型必须支持更新更改的字段的内容。 数据库不执行验证此处在批处理模式下，因此你将需要检查是否有错误，当您调用**UpdateBatch**这种情况下。 某些提供程序还支持 ADO**字段**对象的**UnderlyingValue**和**OriginalValue**属性以帮助你解决冲突，当您试图执行批处理更新。 有关如何解决此类冲突的详细信息，请参阅[编辑数据](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  **记录集字段**追加新时，值不能设置**字段**到**记录集**。 相反，新**字段**可以追加到关闭**记录集**。 则**记录集**必须已打开，并仅然后可以值将分配给这些**字段**。  
  
### <a name="getting-more-field-information"></a>获取更多字段信息  
 ADO 对象有两种类型的属性： 内置和动态。 到目前为止的内置属性仅**字段**讨论了对象。  
  
 内置属性是这些属性在 ADO 中实现，并立即可供任何新对象，请使用`MyObject.Property`语法。 它们不显示为**属性**中对象的对象**属性**集合。  
  
 动态属性定义的基础数据提供程序，并显示在**属性**为适当的 ADO 对象的集合。 例如，特定于所提供的属性可能指示如果**记录集**对象支持事务或更新。 这些附加属性将显示为**属性**中的对象**记录集**对象的**属性**集合。 动态属性可以仅通过集合，并使用语法来引用`MyObject.Properties(0)`或`MyObject.Properties("Name")`。  
  
 无法删除这两种属性。  
  
 动态**属性**对象具有自己的四个内置属性：  
  
-   **名称**属性是一个字符串，标识的属性。  
  
-   **类型**属性是一个整数，指定的属性数据类型。  
  
-   **值**属性是一个包含属性设置的变量。 **值**为默认属性**属性**对象。  
  
-   **属性**属性是**长**值，该值指示特征的特定于所提供的属性。  
  
 **属性**集合**字段**对象包含有关字段的其他元数据。 此集合的内容因提供程序而异。 下面的代码示例检查**属性**集合中的示例**记录集**引入本部分的开头。 它首先查看集合的内容。 此代码使用[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此**属性**集合包含与该提供程序相关的信息。  
  
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
 使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法**字段**填充长二进制或字符数据的对象。 在系统内存有限的情况下，你可以使用**AppendChunk**方法，以操作部分而不是较长的值。  
  
 如果**adFldLong**中位**属性**属性**字段**对象设置为**True**，你可以使用**AppendChunk**该字段的方法。  
  
 第一个**AppendChunk**上调用**字段**对象将数据写入该字段中，覆盖任何现有数据。 后续**AppendChunk**调用添加到现有数据。 如果将数据追加到一个字段，然后设置或读取的当前记录中的另一个字段的值，ADO 假定您已完成了将数据追加到第一个字段。 如果调用**AppendChunk**上再次，第一个字段 ADO 的方法将解释为新的调用**AppendChunk**操作，并覆盖现有数据。 访问在其他字段**记录集**不是克隆的第一个对象**记录集**对象将不会打乱**AppendChunk**操作。  
  
 使用**GetChunk**方法**字段**要检索其长二进制或字符数据的部分或全部对象。 在系统内存有限的情况下，你可以使用**GetChunk**方法，以操作部分，而不是较长的值。  
  
 数据的**GetChunk**调用返回分配给*变量*。 如果*大小*大于剩余的数据， **GetChunk**方法仅返回的剩余数据而无需填充*变量*用空格。 如果该字段为空， **GetChunk**方法返回一个 null 值。  
  
 每个后续**GetChunk**呼叫会检索数据从何处开始以前**GetChunk**调用中断。 但是，如果你从一个字段在检索数据，然后设置或读取的当前记录中的另一个字段的值，ADO 假定完第一个字段从检索数据。 如果调用**GetChunk**上再次，第一个字段 ADO 的方法将解释为新的调用**GetChunk**操作并开始读取数据的起始位置。 访问在其他字段**记录集**不是克隆的第一个对象**记录集**对象将不会打乱**GetChunk**操作。  
  
 如果**adFldLong**中位**属性**属性**字段**对象设置为**True**，你可以使用**GetChunk**该字段的方法。  
  
 如果没有最新记录时你使用**GetChunk**或**AppendChunk**方法**字段**对象时，发生错误 3021 （最新记录）。  
  
 有关使用这些方法用于处理二进制数据的示例，请参阅[AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)中的示例*ADO 程序员参考*。
