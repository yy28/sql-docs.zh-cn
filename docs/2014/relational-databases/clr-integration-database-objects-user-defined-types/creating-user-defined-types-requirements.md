---
title: 用户定义的类型要求 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8cf45c7c108f522f894f97c25ed51bd4dd3c4fbf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970698"
---
# <a name="user-defined-type-requirements"></a>用户定义类型要求
  在创建要安装的用户定义类型（UDT）时，必须做出几个重要的设计决策 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 对于大多数 UDT，建议将 UDT 作为结构创建，尽管也可以选择将其作为类创建。 UDT 定义必须符合用于创建 UDT 的规范，以使其能够注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="requirements-for-implementing-udts"></a>实现 UDT 的要求  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行，您的 UDT 必须实现 UDT 定义中的以下要求：  
  
 该 UDT 必须指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`。 `System.SerializableAttribute` 可选用，但建议使用。  
  
-   UDT 必须通过创建公共的 `System.Data.SqlTypes.INullable`（在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 中为 `static`）`Shared` 方法，在类或结构中实现 `Null` 接口。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 Null 的。 这是为使在 UDT 中执行的代码能够识别 Null 值所必需的。  
  
-   UDT 必须包含支持从其进行分析的公共 `static`（或 `Shared`）`Parse` 方法以及用于转换到对象的字符串表示形式的 `ToString` 方法。  
  
-   具有用户定义序列化格式的 UDT 必须实现 `System.Data.IBinarySerialize` 接口并提供 `Read` 和 `Write` 方法。  
  
-   该 UDT 必须实现 `System.Xml.Serialization.IXmlSerializable`，或者所有公共字段和属性必须均属于 XML 可序列化类型或者使用 `XmlIgnore` 属性进行修饰（如果要求替代标准序列化）。  
  
-   一个 UDT 对象必须只存在一个序列化。 如果序列化或反序列化例程识别了某一特定对象的多个表示形式，则验证将失败。  
  
-   `SqlUserDefinedTypeAttribute.IsByteOrdered` 必须为 `true`，以便按字节顺序比较数据。 如果未实现 IComparable 接口，并且 `SqlUserDefinedTypeAttribute.IsByteOrdered` 为 `false`，字节顺序比较将失败。  
  
-   在类中定义的 UDT 必须具有不采用任何参数的公共构造函数。 您可以选择创建其他重载类构造函数。  
  
-   该 UDT 必须将数据元素作为公共字段或属性过程公开。  
  
-   公共名称的长度不能超过128个字符，并且必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在[数据库标识符](../databases/database-identifiers.md)中定义的标识符的命名规则。  
  
-   `sql_variant` 列不能包含 UDT 的实例。  
  
-   继承的成员无法从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统不知道 UDT 中的继承层次结构。 但是，您可以在创建类的结构时使用继承，并且可以在该类型的托管代码实现方式中调用此类方法。  
  
-   成员不能被重载，但类构造函数除外。 如果您创建某一重载方法，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集或创建类型时将不会引发错误。 在运行时将检测到重载的方法，而不是在创建类型时检测到。 只要永不调用重载的方法，重载的方法就可以存在于类中。 一旦您调用重载的方法，就会引发错误。  
  
-   任何 `static`（或 `Shared`）成员都必须声明为常量或声明为只读。 静态成员将无法改变。  
  
-   如果 `SqlUserDefinedTypeAttribute.MaxByteSize` 字段设置为 -1，则序列化 UDT 在大小上可达到大对象 (LOB) 大小限制（目前为 2 GB）。 该 UDT 的大小不能超过在 `MaxByteSized` 字段中指定的值。  
  
> [!NOTE]  
>  尽管服务器并不使用它来比较性能，但您可以选择实现 `System.IComparable` 接口，该接口公开单个方法 `CompareTo`。 此方法用于客户端上希望精确比较或排序 UDT 值的情况中。  
  
## <a name="native-serialization"></a>本机序列化  
 为您的 UDT 选择正确的序列化属性取决于您正尝试创建的 UDT 的类型。 此 `Native` 序列化格式利用一个非常简单的结构，该结构使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够将 UDT 的有效本机表示形式存储于磁盘上。 如果 UDT 很简单并且只包含以下类型的字段，则建议采用 `Native` 格式：  
  
 **bool**、 **byte**、 **sbyte**、 **short**、 **ushort**、 **int**、 **uint**、 **long**、 **ulong**、 **float**、 **double**、 **SqlByte**、 **SqlInt16**、 **SqlInt32**、 **SqlInt64**、 **SqlDateTime**、 **SqlSingle**、 **SqlDouble**、 **SqlMoney**、 **SqlBoolean**  
  
 由上述类型的字段组成的值类型适用于 `Native` 格式，例如 `structs` 在 Visual c # 中为，或者在 Visual Basic 中 `Structures` 称为。 例如，使用 `Native` 序列化格式指定的 UDT 可包含也用 `Native` 格式指定的其他 UDT 的字段。 如果 UDT 定义更复杂并且包含不在上述列表中的数据类型，则必须改为指定 `UserDefined` 序列化格式。  
  
 `Native` 格式具有以下要求：  
  
-   该类型不能指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize` 的值。  
  
-   所有字段必须均可序列化。  
  
-   如果在类中而不是结构中定义该 UDT，则必须将 `System.Runtime.InteropServices.StructLayoutAttribute` 指定为 `StructLayout.LayoutKindSequential`。 此属性控制数据字段的物理布局，并用来按照成员的出现顺序对它们进行布局。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此属性确定具有多个值的 UDT 的字段顺序。  
  
 有关使用序列化定义的 UDT 的示例 `Native` ，请参阅[编写用户定义类型的代码](creating-user-defined-types-coding.md)中的 Point udt。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 针对 `UserDefined` 属性的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 格式设置为开发人员提供了对二进制格式的完全控制。 在将 `Format` 特性属性指定为 `UserDefined` 时，必须在您的代码中执行以下操作：  
  
-   指定可选的 `IsByteOrdered` 特性属性。 默认值为 `false`。  
  
-   指定 `MaxByteSize` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 属性。  
  
-   编写代码，以便通过实现 `Read` 接口实现 UDT 的 `Write` 方法和 `System.Data.Sql.IBinarySerialize` 方法。  
  
 有关使用序列化定义的 UDT 的示例 `UserDefined` ，请参阅[编写用户定义类型的代码](creating-user-defined-types-coding.md)中的 Currency udt。  
  
> [!NOTE]  
>  为了编制索引，UDT 字段必须使用本机序列化或者是持久化的。  
  
## <a name="serialization-attributes"></a>序列化属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。 在创建 UDT 时，您需要指定 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`。 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 属性指示类是 UDT 并且指定针对 UDT 的存储。 您可以选择指定 `Serializable` 属性，尽管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并不要求这样做。  
  
 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 具有以下属性。  
  
 `Format`  
 指定序列化格式，根据 UDT 的数据类型，该格式可以是 `Native` 或 `UserDefined`。  
  
 `IsByteOrdered`  
 一个 `Boolean` 值，确定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何对 UDT 执行二进制比较。  
  
 `IsFixedLength`  
 指示此 UDT 的所有实例是否都具有相同的长度。  
  
 `MaxByteSize`  
 实例的最大大小（以字节为单位）。 您在指定 `MaxByteSize` 时必须同时指定 `UserDefined` 序列化格式。 对于指定了用户定义的序列化的 UDT，`MaxByteSize` 是指采用用户定义的序列化格式的 UDT 的总大小。 `MaxByteSize` 的值必须处于 1 到 8000 的范围内，或者设置为 -1，以便指示 UDT 大于 8000 字节（总大小不能超过最大 LOB 大小）。 考虑这样一个 UDT：它有一个由 10 个字符组成的字符串属性 (`System.Char`)。 当使用 BinaryWriter 序列化 UDT 时，序列化字符串的总大小为 22 字节：每个 Unicode UTF-16 字符占 2 个字节，乘以最大字符数，再加上因序列化二进制流而导致的系统开销 2 个控制字节。 因此，在确定 `MaxByteSize` 的值时，必须考虑序列化之后的 UDT 的总大小：以二进制格式序列化的数据的大小加上因序列化而导致的系统开销。  
  
 `ValidationMethodName`  
 用于验证 UDT 的实例的方法的名称。  
  
### <a name="setting-isbyteordered"></a>设置 IsByteOrdered  
 如果将 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered` 属性设置为 `true`，则您实际上保证了可以使用已序列化的二进制数据对信息进行语义排序。 因此，以字节排序的 UDT 对象的每个实例只能有一种序列化表示形式。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中对序列化字节执行比较操作时，其结果应与在托管代码中执行同样的比较操作时的结果相同。 如果将 `IsByteOrdered` 设置为 `true`，则还支持以下功能：  
  
-   可以对此类型的列创建索引。  
  
-   可以对此类型的列创建主键和外键以及 CHECK 和 UNIQUE 约束。  
  
-   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 和 PARTITION BY 子句。 此时，将使用该类型的二进制表示形式确定顺序。  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用比较运算符。  
  
-   可以保持此类型的计算列。  
  
 请注意，如果将 `Native` 设置为 `UserDefined`，`IsByteOrdered` 和 `true` 序列化格式将支持以下比较运算符：  
  
-   等于 (=)  
  
-   不等于 (!=)  
  
-   大于号 (>)  
  
-   小于号 (\<)  
  
-   大于或等于 (>=)  
  
-   小于或等于 (&lt;=)  
  
### <a name="implementing-nullability"></a>实现为 Null 性  
 除了正确指定程序集的属性外，类还必须支持为 Null 性。 加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 是可识别 Null 的，但为使 UDT 能够识别某一 Null 值，该类必须实现 `INullable` 接口。 有关如何在 UDT 中实现为空性的详细信息和示例，请参阅[编写用户定义类型的代码](creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字符串转换  
 为了支持与 UDT 之间的字符串转换，必须在类中提供 `Parse` 方法和 `ToString` 方法。 `Parse` 方法允许字符串转换为 UDT。 它必须声明为 `static`（在 Visual Basic 中则为 `Shared`），并且采用 `System.Data.SqlTypes.SqlString` 类型的参数。 有关如何实现和方法的详细信息和示例 `Parse` `ToString` ，请参阅[编写用户定义类型的代码](creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 UDT 必须通过符合针对 XML 序列化的约定，支持与 `xml` 数据类型之间的转换。 `System.Xml.Serialization` 命名空间包含用于将对象序列化为 XML 格式文档或流的类。 您可以选择通过使用 `xml` 接口（该接口为 XML 序列化和反序列化提供自定义格式），实现 `IXmlSerializable` 序列化。  
  
 除了执行从 UDT 到 `xml` 的显式转换外，XML 序列化使您能够：  
  
-   在转换到 `Xquery` 数据类型后使用 UDT 实例的 `xml` 值。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具有本机 XML Web 服务的参数化查询和 Web 方法中使用 UDT。  
  
-   使用 UDT 可以接收 XML 数据的大容量加载。  
  
-   序列化包含具有 UDT 列的表的数据集。  
  
 UDT 在 FOR XML 查询中不序列化。 若要执行显示 UDT 的 XML 序列化的 FOR XML 查询，请在 SELECT 语句中显式将每个 UDT 列转换为 `xml` 数据类型。 您还可以显式将列转换为 `varbinary`、`varchar` 或 `nvarchar`。  
  
## <a name="see-also"></a>另请参阅  
 [Creating a User-Defined Type（创建用户定义类型）](creating-user-defined-types.md)  
  
  
