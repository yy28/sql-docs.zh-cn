---
title: "使用 Visual c + + 扩展 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7722a67ea07a6a5e0b033d8b0131c494e5e6bd11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="visual-c-extensions"></a>Visual c + + 扩展
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 接口
 ADO 关联或绑定，字段的 Microsoft Visual c + + 扩展[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 变量的对象。 每当绑定的当前行**记录集**更改中的所有绑定的字段**记录集**复制到 C/c + + 变量。 如有必要，复制的数据被转换为 C/c + + 变量的声明的数据类型。

 **BindToRecordset**方法**IADORecordBinding**接口将字段绑定到 C/c + + 变量。 **AddNew**方法将新行添加到绑定**记录集**。 **更新**方法填充新的行中的字段**记录集**，或使用 C/c + + 变量的值更新现有行中的字段。

 **IADORecordBinding**接口由实现**记录集**对象。 你不自己代码实现。

## <a name="binding-entries"></a>绑定条目
 ADO 的 Visual c + + 扩展映射的字段[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 变量的对象。 字段和变量之间的映射的定义称为*绑定条目*。 宏提供数字、 固定长度和可变长度数据绑定条目。 从 Visual c + + 扩展类，派生类中声明的绑定项和 C/c + + 变量**CADORecordBinding**。 **CADORecordBinding**通过绑定项宏内部定义类。

 ADO 内部映射中这些宏的参数到 OLE DB **DBBINDING**结构并创建 OLE DB**访问器**要管理的移动和转换的字段和变量之间的数据对象。 OLE DB 将数据定义为包含三个部分组成： 一个*缓冲区*其中的数据存储;*状态*，该值指示是否字段时已成功存储在缓冲区中，还是应还原到的变量的方式字段;与*长度*的数据。 (请参阅[获取文件和设置数据 (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)OLE DB 程序员参考，有关详细信息中。)

## <a name="header-file"></a>标头文件
 为了使用 ADO 的 Visual c + + 扩展应用程序中包括以下文件：

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>绑定的字段记录集

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>为绑定到 C/c + + 变量的字段记录集

1.  创建派生自的类**CADORecordBinding**类。

2.  在派生类中指定绑定项和相应的 C/c + + 变量。 括号之间的绑定项**BEGIN_ADO_BINDING**和**END_ADO_BINDING**宏。 不要终止宏与逗号或分号。 每个宏自动指定适当的分隔符。

     指定的每个字段映射到 C/c + + 变量的一个绑定条目。 使用适当的成员从**ADO_FIXED_LENGTH_ENTRY**， **ADO_NUMERIC_ENTRY**，或**ADO_VARIABLE_LENGTH_ENTRY**系列的宏。

3.  在你的应用程序，创建派生自的类的实例**CADORecordBinding**。 获取**IADORecordBinding**接口从**记录集**。 然后调用**BindToRecordset**方法将绑定**记录集**字段添加到 C/c + + 变量。

 有关详细信息，请参阅[Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md)。

## <a name="interface-methods"></a>接口方法
 **IADORecordBinding**接口有三个方法： **BindToRecordset**， **AddNew**，和**更新**。 为每个方法的唯一自变量是指向派生自的类的实例的**CADORecordBinding**。 因此， **AddNew**和**更新**方法不能指定任何其 ADO 方法 namesakes 的参数。

## <a name="syntax"></a>语法
 **BindToRecordset**方法将关联**记录集**与 C/c + + 变量的字段。

```
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew**方法时，将调用其者同名，ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，以向其中添加新行**记录集**。

```
AddNew(CADORecordBinding *binding)
```

 **更新**方法时，将调用其者同名，ADO[更新](../../../ado/reference/ado-api/update-method.md)方法，来更新**记录集**。

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>绑定项宏
 绑定项宏定义的关联**记录集**字段和变量。 开始和结束宏分隔绑定项的集。

 系列宏提供为固定长度的数据，例如**adDate**或**adBoolean**; 数字数据，如**adTinyInt**， **adInteger**，或**adDouble**; 和可变长度数据，如**每**，**以便您可以排除**或**感**。 所有数值类型，除**adVarNumeric**，也是固定长度的类型。 每个系列具有不同的参数集，以便你可以排除不感兴趣的绑定信息。

 有关详细信息，请参阅[附录 a： 数据类型](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6)的 OLE DB 程序员参考。

### <a name="begin-binding-entries"></a>开始绑定项
 **BEGIN_ADO_BINDING**(*类*)

### <a name="fixed-length-data"></a>固定长度的数据
 **ADO_FIXED_LENGTH_ENTRY**(*序号、 数据类型、 缓冲区、 状态修改*)

 **ADO_FIXED_LENGTH_ENTRY2**(*序号、 数据类型，缓冲区，修改*)

### <a name="numeric-data"></a>数值数据
 **ADO_NUMERIC_ENTRY**(*序号、 数据类型、 缓冲区、 精度、 缩放、 状态，修改*)

 **ADO_NUMERIC_ENTRY2**(*序号、 数据类型、 缓冲区、 精度、 小数位数，修改*)

### <a name="variable-length-data"></a>长度可变的数据
 **ADO_VARIABLE_LENGTH_ENTRY**(*序号、 数据类型、 缓冲区、 大小、 状态、 长度，修改*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*序号、 数据类型、 缓冲区、 大小、 状态，修改*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*序号、 数据类型、 缓冲区、 大小、 长度，修改*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*序号、 数据类型、 缓冲区、 大小，修改*)

### <a name="end-binding-entries"></a>结束绑定项
 **END_ADO_BINDING**（)

|参数|Description|
|---------------|-----------------|
|*类*|在其中定义的绑定项和 C/c + + 变量的类。|
|*Ordinal*|从一个的计数的序号**记录集**字段对应于 C/c + + 变量。|
|*数据类型*|等效的 C/c + + 变量的 ADO 数据类型 (请参阅[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)有关有效的数据类型的列表)。 值**记录集**字段将被转换为此数据类型，如有必要。|
|*缓冲区*|C/c + + 变量的名称其中**记录集**将存储字段。|
|*Size*|最大大小 （字节）*缓冲区*。 如果*缓冲区*将包含可变长度字符串，留出空间的终止字符的零。|
|*“状态”*|将指示的变量名称是否的内容*缓冲区*有效，以及是否的字段的转换*DataType*成功。<br /><br /> 此变量的两个最重要值是**adFldOK**，这意味着转换成功，则和**adFldNull**，这意味着字段的值将是一个变体类型 VT_NULL 并不是仅仅为空。<br /><br /> 可能的值有*状态*列出在下一步的表中，"状态值"。|
|*修改*|布尔型标志。如果为 TRUE，指示允许 ADO 更新相应**记录集**字段中包含的值与*缓冲区*。<br /><br /> 设置布尔值*修改*若要启用 ADO 更新绑定的字段中，为 TRUE 和 FALSE 如果你想要检查该字段，但不是能更改参数。|
|*精度*|可在一个数值变量中表示的数字个数。|
|*小数位数*|一个数值变量中的小数位数的数。|
|*长度*|将包含中的数据的实际长度的 4 字节变量名称*缓冲区*。|

## <a name="status-values"></a>状态值
 值*状态*变量指示是否已成功将一个字段复制到变量。

 当设置数据，*状态*可能设置为**adFldNull**以指示**记录集**字段应设置为 null。

|常量|ReplTest1|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|返回一个非 null 字段值。|
|**adFldBadAccessor**|@shouldalert|绑定句柄无效。|
|**adFldCantConvertValue**|2|符号不匹配或数据溢出之外的原因，无法转换值。|
|**adFldNull**|3|获取字段，指示返回了 null 值。<br /><br /> 当设置字段时，该值指示字段应设置为**NULL**字段不能进行编码时**NULL**本身 （例如，字符数组或一个整数）。|
|**adFldTruncated**|4|长度可变的数据或数字被截断。|
|**adFldSignMismatch**|5|签名值和变量数据类型是无符号。|
|**adFldDataOverFlow**|6|值大于可存储在变量数据类型值。|
|**adFldCantCreate**|7|未知的列类型和字段已打开。|
|**adFldUnavailable**|8|无法确定字段值-例如，在一个新的未分配字段，无默认值上。|
|**adFldPermissionDenied**|9|在更新时，写入数据没有权限。|
|**adFldIntegrityViolation**|10|更新时，字段值违反列完整性。|
|**adFldSchemaViolation**|11|更新时，字段值与列架构冲突。|
|**adFldBadStatus**|12|在更新时，状态参数无效。|
|**adFldDefault**|13|更新时，使用默认值。|

## <a name="see-also"></a>另请参阅
 [Visual c + + 扩展示例](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 扩展标头](../../../ado/guide/appendixes/visual-c-extensions-header.md)
