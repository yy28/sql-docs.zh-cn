---
title: 用户定义的类型要求 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
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
manager: craigg
ms.openlocfilehash: 6faf51099d0a5eced6543704d5f45b6fc922f522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697113"
---
# <a name="creating-user-defined-types---requirements"></a>创建用户定义类型 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在创建用户定义类型 (UDT) 中安装时，必须进行几个重要的设计决策[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 对于大多数 UDT，建议将 UDT 作为结构创建，尽管也可以选择将其作为类创建。 UDT 定义必须符合用于创建 UDT 的规范，以使其能够注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="requirements-for-implementing-udts"></a>实现 UDT 的要求  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行，您的 UDT 必须实现 UDT 定义中的以下要求：  
  
 该 UDT 必须指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。 利用**System.SerializableAttribute**是可选的但建议执行。  
  
-   该 UDT 必须实现**System.Data.SqlTypes.INullable**中的类或结构通过创建一个公共接口**静态**(**共享**中[!INCLUDE[msCoName](../../includes/msconame-md.md)]VisualBasic) **Null**方法。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 Null 的。 这是为使在 UDT 中执行的代码能够识别 Null 值所必需的。  
  
-   UDT 必须包含一个公共**静态**(或**共享**)**分析**支持从其进行分析的方法和公共**ToString**方法将转换为对象的字符串表示形式。  
  
-   使用用户定义序列化格式的 UDT 必须实现**System.Data.IBinarySerialize**接口，并提供**读取**和一个**编写**方法。  
  
-   该 UDT 必须实现**System.Xml.Serialization.IXmlSerializable**，或者所有公共字段和属性必须为这些类型是 XML 可序列化或使用修饰**XmlIgnore**特性重写标准序列化是必需的。  
  
-   一个 UDT 对象必须只存在一个序列化。 如果序列化或反序列化例程识别了某一特定对象的多个表示形式，则验证将失败。  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered**必须是**true**字节顺序中的数据进行比较。 如果未实现 IComparable 接口和**SqlUserDefinedTypeAttribute.IsByteOrdered**是**false**，字节顺序比较将失败。  
  
-   在类中定义的 UDT 必须具有不采用任何参数的公共构造函数。 您可以选择创建其他重载类构造函数。  
  
-   该 UDT 必须将数据元素作为公共字段或属性过程公开。  
  
-   公共名称长度不能超过 128 个字符，并且必须符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中定义的标识符命名规则[数据库标识符](../../relational-databases/databases/database-identifiers.md)。  
  
-   **sql_variant**列不能包含 UDT 的实例。  
  
-   继承的成员无法从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统不知道 UDT 中的继承层次结构。 但是，您可以在创建类的结构时使用继承，并且可以在该类型的托管代码实现方式中调用此类方法。  
  
-   成员不能被重载，但类构造函数除外。 如果您创建某一重载方法，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集或创建类型时将不会引发错误。 在运行时将检测到重载的方法，而不是在创建类型时检测到。 只要永不调用重载的方法，重载的方法就可以存在于类中。 一旦您调用重载的方法，就会引发错误。  
  
-   任何**静态**(或**共享**) 成员必须声明为常量或为只读的。 静态成员将无法改变。  
  
-   如果**SqlUserDefinedTypeAttribute.MaxByteSize**字段设置为-1，则序列化的 UDT 可以大至作为大型对象 (LOB) 大小限制 (目前为 2 GB)。 该 UDT 的大小不能超过中指定的值**MaxByteSized**字段。  
  
> [!NOTE]  
>  尽管它不由服务器来执行比较，您可以选择实现**System.IComparable**接口，公开了一个方法，该接口**CompareTo**。 此方法用于客户端上希望精确比较或排序 UDT 值的情况中。  
  
## <a name="native-serialization"></a>本机序列化  
 为您的 UDT 选择正确的序列化属性取决于您正尝试创建的 UDT 的类型。 **本机**序列化格式利用一个非常简单的结构，使[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]磁盘上存储 UDT 的有效本机表示形式。 **本机**如果 UDT 很简单，仅包含以下类型的字段，建议使用格式：  
  
 **bool**，**字节**， **sbyte**，**短**， **ushort**， **int**， **uint**，**长**， **ulong**， **float**， **double**，**以**，**SqlInt16**， **SqlInt32**， **SqlInt64**， **SqlDateTime**， **SqlSingle**， **SqlDouble**， **SqlMoney**， **SqlBoolean**  
  
 值类型，构成上述类型的字段的非常适合进行**本机**格式，例如**结构**在 Visual C# 中，(或**结构**大家所熟知中Visual Basic 中)。 例如，使用指定的 UDT**本机**序列化格式可能包含的其他 UDT 的使用也指定了字段**本机**格式。 如果 UDT 定义更复杂，包含不在上述列表的数据类型，必须指定**UserDefined**改为序列化格式。  
  
 **本机**格式具有以下要求：  
  
-   类型必须为指定值**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**。  
  
-   所有字段必须均可序列化。  
  
-   **System.Runtime.InteropServices.StructLayoutAttribute**必须指定为**StructLayout.LayoutKindSequential**如果 UDT 定义一个类，而不是结构中。 此属性控制数据字段的物理布局，并用来按照成员的出现顺序对它们进行布局。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此属性确定具有多个值的 UDT 的字段顺序。  
  
 有关使用定义的 UDT 的示例**本机**序列化，请参阅中的 Point UDT[类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **UserDefined**格式设置为**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性将使开发人员完全控制二进制格式。 指定时**格式**特性的属性作为**UserDefined**，必须在代码中执行以下操作：  
  
-   指定可选**IsByteOrdered**特性属性。 默认值是 **false**秒。  
  
-   指定**MaxByteSize**的属性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。  
  
-   编写代码以实现**读**并**编写**用于通过实现 UDT 方法**System.Data.Sql.IBinarySerialize**接口。  
  
 有关使用定义的 UDT 的示例**UserDefined**序列化，请参阅中的 Currency UDT[类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
> [!NOTE]  
>  为了编制索引，UDT 字段必须使用本机序列化或者是持久化的。  
  
## <a name="serialization-attributes"></a>序列化属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。 需要指定**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**时创建用户定义的类型。 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**属性指示类是 UDT 并且指定的 UDT 的存储。 您可以选择指定**Serializable**属性，尽管[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不需要它。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**具有以下属性。  
  
 **格式**  
 指定序列化格式，可以是**本机**或**UserDefined**，取决于用户定义的类型的数据类型。  
  
 **IsByteOrdered**  
 一个**布尔**值，该值确定如何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对 UDT 执行二进制比较。  
  
 **IsFixedLength**  
 指示此 UDT 的所有实例是否都具有相同的长度。  
  
 **MaxByteSize**  
 实例的最大大小（以字节为单位）。 必须指定**MaxByteSize**与**UserDefined**序列化格式。 有关与指定，用户定义序列化 UDT **MaxByteSize**定义的用户是指其序列化的窗体中的 UDT 的总大小。 值**MaxByteSize**必须在 1 到 8000 的范围内或设置为-1 以指示 UDT 大于 8000 个字节 （总大小不能超过最大 LOB 大小）。 考虑这样一个 UDT 属性值为 10 个字符的字符串 (**System.Char**)。 当使用 BinaryWriter 序列化 UDT 时，序列化字符串的总大小为 22 字节：每个 Unicode UTF-16 字符占 2 个字节，乘以最大字符数，再加上因序列化二进制流而导致的系统开销 2 个控制字节。 因此，确定的值时**MaxByteSize**，必须考虑序列化 UDT 的总大小： 以二进制格式序列化的数据加上因序列化所产生的开销大小。  
  
 **ValidationMethodName**  
 用于验证 UDT 的实例的方法的名称。  
  
### <a name="setting-isbyteordered"></a>设置 IsByteOrdered  
 当**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered**属性设置为**true**，实际上保证的序列化的二进制数据，可以用于语义排序的信息。 因此，以字节排序的 UDT 对象的每个实例只能有一种序列化表示形式。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中对序列化字节执行比较操作时，其结果应与在托管代码中执行同样的比较操作时的结果相同。 以下功能均支持何时**IsByteOrdered**设置为**true**:  
  
-   可以对此类型的列创建索引。  
  
-   可以对此类型的列创建主键和外键以及 CHECK 和 UNIQUE 约束。  
  
-   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 和 PARTITION BY 子句。 此时，将使用该类型的二进制表示形式确定顺序。  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用比较运算符。  
  
-   可以保持此类型的计算列。  
  
 请注意，同时**本机**并**UserDefined**序列化格式支持以下比较运算符时**IsByteOrdered**设置为 **，则返回 true**:  
  
-   等于 (=)  
  
-   不等于 (!=)  
  
-   大于号 (>)  
  
-   小于号 (\<)  
  
-   大于或等于 (> =)  
  
-   小于或等于 (<=)  
  
### <a name="implementing-nullability"></a>实现为 Null 性  
 除了正确指定程序集的属性外，类还必须支持为 Null 性。 加载到 Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是可识别 null 的但为了使 UDT 能够识别 null 值，该类必须实现**INullable**接口。 有关详细信息和如何在 UDT 中实现为 null 性的示例，请参阅[类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字符串转换  
 若要支持字符串转换到和从 UDT，必须提供**分析**方法和一个**ToString**中您的类的方法。 **分析**方法允许将字符串转换为 UDT。 它必须声明为**静态**(或**共享**在 Visual Basic 中)，并且采用的类型参数**System.Data.SqlTypes.SqlString**。 有关详细信息和如何实现的示例**分析**并**ToString**方法，请参阅[类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 Udt 必须支持转换来回**xml**通过符合 XML 序列化协定的数据类型。 **System.Xml.Serialization**命名空间包含用于对象序列化为 XML 格式的文档或流的类。 您可以选择实施**xml**使用的序列化**IXmlSerializable**接口，以便进行 XML 序列化和反序列化提供自定义格式设置。  
  
 除了执行从 UDT 到的显式转换**xml**，XML 序列化使你能够：  
  
-   使用**Xquery** UDT 后的实例转换为值**xml**数据类型。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具有本机 XML Web 服务的参数化查询和 Web 方法中使用 UDT。  
  
-   使用 UDT 可以接收 XML 数据的大容量加载。  
  
-   序列化包含具有 UDT 列的表的数据集。  
  
 UDT 在 FOR XML 查询中不序列化。 若要执行显示 Udt 的 XML 序列化的 FOR XML 查询，显式转换为每个 UDT 列**xml** SELECT 语句中的数据类型。 可以显式转换到的列**varbinary**， **varchar**，或**nvarchar**。  
  
## <a name="see-also"></a>请参阅  
 [创建用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
