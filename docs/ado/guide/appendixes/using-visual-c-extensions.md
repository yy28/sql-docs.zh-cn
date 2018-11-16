---
title: 使用 Visual c + + 扩展 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeae626f924776092bc8f6652e716747768b689c
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350521"
---
# <a name="visual-c-extensions"></a>Visual c + + 扩展
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 接口
 ADO 关联或绑定，字段的 Microsoft Visual c + + 扩展[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到 C/c + + 变量的对象。 只要绑定的当前行**记录集**发生更改中的所有绑定的字段**记录集**复制到 C/c + + 变量。 如有必要，复制的数据转换为 C/c + + 变量声明的数据类型。

 **BindToRecordset**方法**IADORecordBinding**接口将字段绑定到 C/c + + 变量。 **AddNew**方法将新行添加到绑定**记录集**。 **更新**方法填充新的行中的字段**记录集**，或使用 C/c + + 变量的值更新现有行中的字段。

 **IADORecordBinding**接口由实现**记录集**对象。 你不自己编码实现。

## <a name="binding-entries"></a>绑定条目
 ADO 的 Visual c + + 扩展的字段映射[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)到 C/c + + 变量的对象。 调用字段和变量之间的映射的定义*绑定条目*。 宏提供数值、 固定长度和可变长度数据绑定项。 在 Visual c + + 扩展类，派生类中声明绑定项和 C/c + + 变量**CADORecordBinding**。 **CADORecordBinding**类在内部由绑定项宏。

 ADO 在内部将这些宏中的参数映射到 OLE DB **DBBINDING**结构，并创建 OLE DB**访问器**对象来管理移动和数据字段和变量之间的转换。 OLE DB 数据定义为包含三个部分： 一个*缓冲区*数据存储;*状态*，该值指示是否字段已成功存储在缓冲区中或如何将变量应还原到字段;并*长度*的数据。 (请参阅[获取文件和设置数据 (OLE DB)](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369)中的 OLE DB 程序员参考，有关详细信息。)

## <a name="header-file"></a>标头文件
 若要使用 ADO 的 Visual c + + 扩展应用程序中包括以下文件：

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>绑定的记录集字段

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>若要将记录集字段绑定到 C/c + + 变量

1.  创建派生自的类**CADORecordBinding**类。

2.  在派生类中指定绑定项和相应的 C/c + + 变量。 括号之间的绑定条目**BEGIN_ADO_BINDING**并**END_ADO_BINDING**宏。 不要终止之间用逗号或分号的宏。 每个宏自动指定适当的分隔符。

     指定要映射到 C/c + + 变量的每个字段的一个绑定项。 使用从适当的成员**ADO_FIXED_LENGTH_ENTRY**， **ADO_NUMERIC_ENTRY**，或**ADO_VARIABLE_LENGTH_ENTRY**系列的宏。

3.  在应用程序中，创建派生自的类的实例**CADORecordBinding**。 获取**IADORecordBinding**从接口**记录集**。 然后调用**BindToRecordset**方法绑定**记录集**到 C/c + + 变量字段。

 有关详细信息，请参阅[Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)。

## <a name="interface-methods"></a>接口方法
 **IADORecordBinding**接口有三个方法： **BindToRecordset**， **AddNew**，以及**更新**。 每个方法的唯一参数是指向派生自的类的实例的指针**CADORecordBinding**。 因此， **AddNew**并**更新**方法不能指定任何其 ADO 方法 namesakes 的参数。

## <a name="syntax"></a>语法
 **BindToRecordset**方法相关联**记录集**与 C/c + + 变量字段。

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew**方法将调用其作用，ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，以向其中添加新行**记录集**。

```cpp
AddNew(CADORecordBinding *binding)
```

 **更新**方法将调用其作用，ADO[更新](../../../ado/reference/ado-api/update-method.md)方法，以更新**记录集**。

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>绑定项宏
 绑定项宏定义的关联**记录集**字段和变量。 开始和结束宏分隔绑定项集。

 为固定长度的数据，如提供系列宏**adDate**或**adBoolean**; 数值数据，如**adTinyInt**， **adInteger**，或**adDouble**; 和可变长度数据，如**每**，**以便您可以排除**或**adVarBinary**。 所有数值类型，除了**adVarNumeric**，也是固定长度类型。 每个系列具有不同的参数集，以便您可以排除不感兴趣的绑定信息。

 有关详细信息，请参阅[附录 a： 数据类型](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6)的 OLE DB 程序员参考。

### <a name="begin-binding-entries"></a>开始绑定项
 **BEGIN_ADO_BINDING**(*类*)

### <a name="fixed-length-data"></a>固定长度的数据
 **ADO_FIXED_LENGTH_ENTRY**(*序号、 数据类型、 缓冲区、 状态修改*)

 **ADO_FIXED_LENGTH_ENTRY2**(*序号、 数据类型，缓冲区中，修改*)

### <a name="numeric-data"></a>数值数据
 **ADO_NUMERIC_ENTRY**(*序号、 数据类型、 缓冲区、 精度、 小数位数、 状态修改*)

 **ADO_NUMERIC_ENTRY2**(*序号、 数据类型、 缓冲区、 精度和小数位数，修改*)

### <a name="variable-length-data"></a>长度可变的数据
 **ADO_VARIABLE_LENGTH_ENTRY**(*序号、 数据类型、 缓冲区、 大小、 状态、 长度、 修改*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*序号、 数据类型、 缓冲区、 大小、 状态修改*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*序号、 数据类型、 缓冲区、 大小、 长度、 修改*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*序号、 数据类型、 缓冲区、 大小、 修改*)

### <a name="end-binding-entries"></a>结束绑定项
 **END_ADO_BINDING**()

|参数|Description|
|---------------|-----------------|
|*类*|在其中定义的绑定项和 C/c + + 变量的类。|
|*Ordinal*|一个中，对计数的序号**记录集**字段对应于 C/c + + 变量。|
|*DataType*|C/c + + 变量等效 ADO 数据类型 (请参阅[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)有关有效的数据类型的列表)。 值**记录集**字段将转换为此数据类型，如有必要。|
|*Buffer*|C/c + + 变量的名称，**记录集**将存储字段。|
|*大小*|以字节为单位的最大大小*缓冲区*。 如果*缓冲区*将包含可变长度字符串，留出了为终止字符的零。|
|*“状态”*|将指示变量的名称是否的内容*缓冲区*有效，以及是否对字段的转换*数据类型*是否成功。<br /><br /> 此变量的两个最重要的值是**adFldOK**，这意味着转换成功，则和**adFldNull**，这意味着字段的值将为类型 VT_NULL 的变体，而不仅仅是为空。<br /><br /> 可能的值*状态*列出在下一步的表中，"状态值"。|
|*修改*|布尔型标志。如果为 TRUE，指示允许 ADO 更新相应**记录集**字段中包含的值*缓冲区*。<br /><br /> 设置一个布尔值*修改*参数为 TRUE，为了使 ADO 能够更新字段绑定，且如果你想要检查该字段，但不能更改它，则为 FALSE。|
|*精度*|可在数值变量中表示的数字的位数。|
|*小数位数*|数值变量中的小数位数。|
|*长度*|将包含中的数据的实际长度的 4 字节变量的名称*缓冲区*。|

## <a name="status-values"></a>状态值
 值*状态*变量指示是否已成功将一个字段复制到一个变量。

 设置数据时*状态*可能会设置为**adFldNull**指示**记录集**字段应设置为 null。

|常量|ReplTest1|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|返回非 null 字段值。|
|**adFldBadAccessor**|1|绑定无效。|
|**adFldCantConvertValue**|2|无法转换值，而原因并非符号不匹配或数据溢出。|
|**adFldNull**|3|一个字段时，指示返回了 null 值。<br /><br /> 当设置的字段，指示该字段应设置为**NULL**对该字段不能进行编码**NULL**本身 （例如，字符数组或整数）。|
|**adFldTruncated**|4|数字位数或长度可变的数据已被截断。|
|**adFldSignMismatch**|5|签名值和变量数据类型是无符号。|
|**adFldDataOverFlow**|6|值为大于可能存储在变量数据类型。|
|**adFldCantCreate**|7|未知的列类型和字段已打开。|
|**adFldUnavailable**|8|无法确定字段值-例如，在新的、 未分配的字段，没有默认值。|
|**adFldPermissionDenied**|9|在更新时，没有写入数据的权限。|
|**adFldIntegrityViolation**|10|在更新时，字段值与列的完整性冲突。|
|**adFldSchemaViolation**|11|在更新时，字段值与列架构冲突。|
|**adFldBadStatus**|12|在更新时，无效的状态参数。|
|**adFldDefault**|13|在更新时，使用默认值。|

## <a name="see-also"></a>请参阅
 [Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)
