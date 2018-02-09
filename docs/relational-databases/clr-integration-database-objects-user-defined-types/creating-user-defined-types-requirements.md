---
title: "用户定义的类型要求 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a075d6c4c4cc5ccd0477bb33159cf319fb0754b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="creating-user-defined-types---requirements"></a>创建用户定义的类型的要求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
创建用户定义类型 (UDT) 中安装时，必须进行一些重要的设计决策[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 对于大多数 UDT，建议将 UDT 作为结构创建，尽管也可以选择将其作为类创建。 UDT 定义必须符合用于创建 UDT 的规范，以使其能够注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="requirements-for-implementing-udts"></a>实现 UDT 的要求  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行，您的 UDT 必须实现 UDT 定义中的以下要求：  
  
 用户定义的类型必须指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。 使用**System.SerializableAttribute**是可选的但建议使用。  
  
-   用户定义的类型必须实现**System.Data.SqlTypes.INullable**中的类或结构通过创建一个公共接口**静态**(**共享**中[!INCLUDE[msCoName](../../includes/msconame-md.md)]VisualBasic) **Null**方法。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 Null 的。 这是为使在 UDT 中执行的代码能够识别 Null 值所必需的。  
  
-   用户定义的类型必须包含一个公共**静态**(或**共享**)**分析**支持，从分析的方法和公共**ToString**方法将转换为字符串对象的表示形式。  
  
-   必须实现的用户定义序列化格式与 UDT **System.Data.IBinarySerialize**接口，并提供**读取**和**编写**方法。  
  
-   用户定义的类型必须实现**System.Xml.Serialization.IXmlSerializable**，或者所有公共字段和属性必须是这些类型包含 XML 可序列化或与修饰**XmlIgnore**属性如果重写标准序列化是必需的。  
  
-   一个 UDT 对象必须只存在一个序列化。 如果序列化或反序列化例程识别了某一特定对象的多个表示形式，则验证将失败。  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered**必须**true**在字节顺序中的数据进行比较。 如果未实现 IComparable 接口和**SqlUserDefinedTypeAttribute.IsByteOrdered**是**false**，字节顺序比较将会失败。  
  
-   在类中定义的 UDT 必须具有不采用任何参数的公共构造函数。 您可以选择创建其他重载类构造函数。  
  
-   该 UDT 必须将数据元素作为公共字段或属性过程公开。  
  
-   公共名称长度不能超过 128 个字符，并且必须符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中定义的标识符的命名规则[数据库标识符](../../relational-databases/databases/database-identifiers.md)。  
  
-   **sql_variant**列不能包含 UDT 的实例。  
  
-   继承的成员无法从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统不知道 UDT 中的继承层次结构。 但是，您可以在创建类的结构时使用继承，并且可以在该类型的托管代码实现方式中调用此类方法。  
  
-   成员不能被重载，但类构造函数除外。 如果您创建某一重载方法，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集或创建类型时将不会引发错误。 在运行时将检测到重载的方法，而不是在创建类型时检测到。 只要永不调用重载的方法，重载的方法就可以存在于类中。 一旦您调用重载的方法，就会引发错误。  
  
-   任何**静态**(或**共享**) 成员必须声明为常量或为只读。 静态成员将无法改变。  
  
-   如果**SqlUserDefinedTypeAttribute.MaxByteSize**字段设置为-1、 用户定义的序列化的类型可以是一样大的大型对象 (LOB) 大小限制 (当前为 2 GB)。 用户定义的类型的大小不能超过中指定的值**MaxByteSized**字段。  
  
> [!NOTE]  
>  尽管它不用于服务器执行比较，你可以选择实现**System.IComparable**接口，公开一种方法，该接口**CompareTo**。 此方法用于客户端上希望精确比较或排序 UDT 值的情况中。  
  
## <a name="native-serialization"></a>本机序列化  
 为您的 UDT 选择正确的序列化属性取决于您正尝试创建的 UDT 的类型。 **本机**序列化格式利用一个非常简单的结构，它使[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT 的有效本机表示存储在磁盘上。 **本机**如果 UDT 很简单，仅包含以下类型的字段，建议使用格式：  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 值类型组成上述所有类型的字段的非常适合进行**本机**格式，如**结构**在 Visual C# 中，(或**结构**中称之为Visual Basic 中)。 例如，UDT 指定**本机**序列化格式可能包含的另一个还已使用指定的 UDT 字段**本机**格式。 如果在 UDT 定义更复杂且包含数据类型不是在上面的列表中，你必须指定**用户定制**改为序列化格式。  
  
 **本机**格式具有以下要求：  
  
-   该类型必须不指定的值**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**。  
  
-   所有字段必须均可序列化。  
  
-   **System.Runtime.InteropServices.StructLayoutAttribute**必须指定为**StructLayout.LayoutKindSequential**如果一个类和不是在结构中定义用户定义的类型。 此属性控制数据字段的物理布局，并用来按照成员的出现顺序对它们进行布局。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此属性确定具有多个值的 UDT 的字段顺序。  
  
 UDT 的示例定义与**本机**序列化，请参阅中点 UDT [Coding User-Defined 类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **用户定制**格式设置**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性将使开发人员完全控制的二进制格式。 指定时**格式**特性属性作为**用户定制**，你必须在代码中执行以下操作：  
  
-   指定可选**IsByteOrdered**特性属性。 默认值是 **false**秒。  
  
-   指定**MaxByteSize**属性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。  
  
-   编写代码以实现**读取**和**编写**用于通过实现 UDT 方法**System.Data.Sql.IBinarySerialize**接口。  
  
 UDT 的示例定义与**用户定制**序列化，请参阅在货币 UDT [Coding User-Defined 类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
> [!NOTE]  
>  为了编制索引，UDT 字段必须使用本机序列化或者是持久化的。  
  
## <a name="serialization-attributes"></a>序列化属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。 将要求你指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**时创建用户定义的类型。 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性指示类是 UDT 的并且指定存储的用户定义的类型。 你可以选择指定**Serializable**特性，虽然[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不需要它。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**具有以下属性。  
  
 **格式**  
 指定的序列化格式，它可以是**本机**或**用户定制**，取决于用户定义的类型的数据类型。  
  
 **IsByteOrdered**  
 A**布尔**值，该值确定如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT 上执行二进制比较。  
  
 **IsFixedLength**  
 指示此 UDT 的所有实例是否都具有相同的长度。  
  
 **MaxByteSize**  
 实例的最大大小（以字节为单位）。 必须指定**MaxByteSize**与**用户定制**序列化格式。 有关与用户定义的序列化指定，UDT **MaxByteSize**指由用户定义的序列化形式 UDT 的总大小。 值**MaxByteSize**必须在 1 到 8000 的范围内或设置为-1 以指示 UDT 大于 8000 个字节 （总大小不能超过最大的 LOB 大小）。 考虑这样一个 UDT 属性值为 10 个字符的字符串 (**System.Char**)。 当使用 BinaryWriter 序列化 UDT 时，序列化字符串的总大小为 22 字节：每个 Unicode UTF-16 字符占 2 个字节，乘以最大字符数，再加上因序列化二进制流而导致的系统开销 2 个控制字节。 因此，在确定的值时**MaxByteSize**，必须考虑用户定义的序列化类型的总大小： 的大小以二进制格式序列化的数据加上序列化所需的开销。  
  
 **ValidationMethodName**  
 用于验证 UDT 的实例的方法的名称。  
  
### <a name="setting-isbyteordered"></a>设置 IsByteOrdered  
 当**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered**属性设置为**true**，实际上，可以用于序列化的二进制数据，从而保证语义排序的信息。 因此，以字节排序的 UDT 对象的每个实例只能有一种序列化表示形式。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中对序列化字节执行比较操作时，其结果应与在托管代码中执行同样的比较操作时的结果相同。 以下功能也是当**IsByteOrdered**设置为**true**:  
  
-   可以对此类型的列创建索引。  
  
-   可以对此类型的列创建主键和外键以及 CHECK 和 UNIQUE 约束。  
  
-   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 和 PARTITION BY 子句。 此时，将使用该类型的二进制表示形式确定顺序。  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用比较运算符。  
  
-   可以保持此类型的计算列。  
  
 请注意，同时**本机**和**用户定制**序列化格式支持以下比较运算符时**IsByteOrdered**设置为**true**:  
  
-   等于 (=)  
  
-   不等于 (!=)  
  
-   大于号 (>)  
  
-   小于号 (\<)  
  
-   大于或等于 (> =)  
  
-   小于或等于 (<=)  
  
### <a name="implementing-nullability"></a>实现为 Null 性  
 除了正确指定程序集的属性外，类还必须支持为 Null 性。 加载到 Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]都是 null 感知，类必须实现使 UDT 识别 null 值，但**INullable**接口。 有关详细信息和如何在 UDT 中实现为空性的示例，请参阅[Coding User-Defined 类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字符串转换  
 若要支持与其他用户定义的类型的字符串转换，必须提供**分析**方法和一个**ToString**类中的方法。 **分析**方法允许将字符串转换为 UDT。 它必须声明为**静态**(或**共享**在 Visual Basic 中)，并采取类型的参数**System.Data.SqlTypes.SqlString**。 有关详细信息和举例说明如何实现**分析**和**ToString**方法，请参阅[Coding User-Defined 类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 Udt 必须支持转换到和从**xml**通过符合 XML 序列化协定的数据类型。 **System.Xml.Serialization**命名空间包含用于对象序列化为 XML 格式的文档或流的类。 你可以选择实现**xml**使用的序列化**IXmlSerializable**接口，从而为 XML 序列化和反序列化提供自定义格式设置。  
  
 除了执行从到 UDT 的显式转换**xml**，XML 序列化，您可以：  
  
-   使用**Xquery**的转换后的 UDT 实例的值通过**xml**数据类型。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具有本机 XML Web 服务的参数化查询和 Web 方法中使用 UDT。  
  
-   使用 UDT 可以接收 XML 数据的大容量加载。  
  
-   序列化包含具有 UDT 列的表的数据集。  
  
 UDT 在 FOR XML 查询中不序列化。 若要执行显示的 XML 序列化 Udt 的 FOR XML 查询，显式转换到每个 UDT 列**xml** SELECT 语句中的数据类型。 你可以将还显式转换到的列**varbinary**， **varchar**，或**nvarchar**。  
  
## <a name="see-also"></a>另请参阅  
 [创建的用户定义的类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
