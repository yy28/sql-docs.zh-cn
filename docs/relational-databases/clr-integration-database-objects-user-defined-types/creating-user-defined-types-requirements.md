---
title: 用户定义的类型要求 |Microsoft Docs
description: 本文介绍了在创建要安装在 SQL Server 上的 UDT 时需要进行的重要设计决策。
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
ms.openlocfilehash: b20192a3804dfba713b04706d528738ceb8768c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727807"
---
# <a name="creating-user-defined-types---requirements"></a>创建用户定义类型 - 需求
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  在创建要安装的用户定义类型（UDT）时，必须做出几个重要的设计决策 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 对于大多数 UDT，建议将 UDT 作为结构创建，尽管也可以选择将其作为类创建。 UDT 定义必须符合用于创建 UDT 的规范，以使其能够注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="requirements-for-implementing-udts"></a>实现 UDT 的要求  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行，您的 UDT 必须实现 UDT 定义中的以下要求：  
  
 该 UDT 必须指定**SqlUserDefinedTypeAttribute**。 **SerializableAttribute**的使用是可选的，但建议使用。  
  
-   UDT 必须通过创建公共**静态**（在 Visual Basic 中为**共享**） Null 方法来实现类或结构中的**SqlTypes。** [!INCLUDE[msCoName](../../includes/msconame-md.md)] **Null** 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 Null 的。 这是为使在 UDT 中执行的代码能够识别 Null 值所必需的。  
  
-   UDT 必须包含一个公共**静态**（或**共享**）**分析**方法，该方法支持从中进行分析，以及一个公共**ToString**方法，用于转换为对象的字符串表示形式。  
  
-   使用用户定义的序列化格式的 UDT 必须实现**IBinarySerialize**接口并提供**读****写**方法。  
  
-   UDT 必须实现**System.Xml。** 如果需要重写标准序列化，则串行化或所有公共字段和属性必须是 XML 可序列化的类型或用**XmlIgnore**特性修饰的类型。  
  
-   一个 UDT 对象必须只存在一个序列化。 如果序列化或反序列化例程识别了某一特定对象的多个表示形式，则验证将失败。  
  
-   若要按字节顺序比较数据，SqlUserDefinedTypeAttribute 必须为**true** **。** 如果未实现 IComparable 接口并且**SqlUserDefinedTypeAttribute**为**false**，则字节顺序比较将失败。  
  
-   在类中定义的 UDT 必须具有不采用任何参数的公共构造函数。 您可以选择创建其他重载类构造函数。  
  
-   该 UDT 必须将数据元素作为公共字段或属性过程公开。  
  
-   公共名称的长度不能超过128个字符，并且必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在[数据库标识符](../../relational-databases/databases/database-identifiers.md)中定义的标识符的命名规则。  
  
-   **sql_variant**列不能包含 UDT 的实例。  
  
-   继承的成员无法从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统不知道 UDT 中的继承层次结构。 但是，您可以在创建类的结构时使用继承，并且可以在该类型的托管代码实现方式中调用此类方法。  
  
-   成员不能被重载，但类构造函数除外。 如果您创建某一重载方法，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集或创建类型时将不会引发错误。 在运行时将检测到重载的方法，而不是在创建类型时检测到。 只要永不调用重载的方法，重载的方法就可以存在于类中。 一旦您调用重载的方法，就会引发错误。  
  
-   任何**静态**（或**共享**）成员都必须声明为常量或只读。 静态成员将无法改变。  
  
-   如果将**SqlUserDefinedTypeAttribute MaxByteSize**字段设置为-1，则序列化的 UDT 的大小可能与大型对象（LOB）大小限制（目前为 2 GB）大。 UDT 的大小不能超过在**MaxByteSized**字段中指定的值。  
  
> [!NOTE]  
>  尽管服务器不使用它来执行比较，但你可以选择实现**system.icomparable**接口，该接口公开单一方法**CompareTo**。 此方法用于客户端上希望精确比较或排序 UDT 值的情况中。  
  
## <a name="native-serialization"></a>本机序列化  
 为您的 UDT 选择正确的序列化属性取决于您正尝试创建的 UDT 的类型。 **本机**序列化格式使用非常简单的结构，该结构使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够在磁盘上存储 UDT 的有效本机表示形式。 如果 UDT 非常简单且仅包含以下类型的字段，则建议使用**本机**格式：  
  
 **bool**、 **byte**、 **sbyte**、 **short**、 **ushort**、 **int**、 **uint**、 **long**、 **ulong**、 **float**、 **double**、 **SqlByte**、 **SqlInt16**、 **SqlInt32**、 **SqlInt64**、 **SqlDateTime**、 **SqlSingle**、 **SqlDouble**、 **SqlMoney**、 **SqlBoolean**  
  
 由上述类型的字段组成的值类型适用于**本机**格式（如 Visual c # 中的**结构**）（或在 Visual Basic 中已知的**结构**。） 例如，使用**本机**序列化格式指定的 udt 可以包含另一个 UDT 的字段，该字段也是使用**本机**格式指定的。 如果 UDT 定义更复杂并且包含不在上述列表中的数据类型，则必须改为指定**用户**定义的序列化格式。  
  
 **本机**格式具有以下要求：  
  
-   该类型不得为**SqlUserDefinedTypeAttribute. MaxByteSize**指定值。  
  
-   所有字段必须均可序列化。  
  
-   如果 UDT 是在类中定义的，而不是在结构中定义的，则必须将**InteropServices**指定为**StructLayout。** 此属性控制数据字段的物理布局，并用来按照成员的出现顺序对它们进行布局。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此属性确定具有多个值的 UDT 的字段顺序。  
  
 有关使用**本机**序列化定义的 udt 的示例，请参阅[编写用户定义类型的代码](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的 Point udt。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **SqlUserDefinedTypeAttribute**特性的**用户**设置的格式设置使开发人员可以完全控制二进制格式。 以**用户用户**身份指定**格式**属性属性时，必须在代码中执行以下操作：  
  
-   指定可选的**IsByteOrdered**特性属性。 默认值是 **false**秒。  
  
-   指定**SqlUserDefinedTypeAttribute**的 " **MaxByteSize** " 属性。  
  
-   通过实现**IBinarySerialize**接口，编写代码来实现 UDT 的**读取**和**写入**方法。  
  
 有关使用**用户**定义的序列化定义的 UDT 的示例，请参阅[编写用户定义类型的代码](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的 Currency udt。  
  
> [!NOTE]  
>  为了编制索引，UDT 字段必须使用本机序列化或者是持久化的。  
  
## <a name="serialization-attributes"></a>序列化属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。 创建 UDT 时，您需要指定**SqlUserDefinedTypeAttribute**的。 **SqlUserDefinedTypeAttribute**特性指示类为 udt，并指定 udt 的存储。 "。 您可以选择指定**可序列化**属性，但不 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要此属性。  
  
 **SqlUserDefinedTypeAttribute**包含以下属性：。  
  
 **格式**  
 指定序列化格式，它可以是**本机**的，也可以是**用户定制**的，具体取决于 UDT 的数据类型。  
  
 **IsByteOrdered**  
 确定**Boolean**如何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对 UDT 执行二进制比较的布尔值。  
  
 **IsFixedLength**  
 指示此 UDT 的所有实例是否都具有相同的长度。  
  
 **MaxByteSize**  
 实例的最大大小（以字节为单位）。 必须用**用户定制**的序列化格式指定**MaxByteSize** 。 对于指定了用户定义的序列化的 UDT， **MaxByteSize**是指由用户定义的序列化格式的 udt 的总大小。 **MaxByteSize**的值必须在1到8000的范围内，或设置为-1 以指示 UDT 大于8000字节（总大小不能超过最大 LOB 大小）。 请考虑使用包含10个**字符（system.string**）的字符串的属性的 UDT。 当使用 BinaryWriter 序列化 UDT 时，序列化字符串的总大小为 22 字节：每个 Unicode UTF-16 字符占 2 个字节，乘以最大字符数，再加上因序列化二进制流而导致的系统开销 2 个控制字节。 因此，在确定**MaxByteSize**的值时，必须考虑序列化 UDT 的总大小：以二进制格式序列化的数据的大小加上序列化导致的开销。  
  
 **ValidationMethodName**  
 用于验证 UDT 的实例的方法的名称。  
  
### <a name="setting-isbyteordered"></a>设置 IsByteOrdered  
 如果将**SqlUserDefinedTypeAttribute**属性设置为**true**，则会有效地确保序列化的二进制数据可用于信息的语义顺序排序。 因此，以字节排序的 UDT 对象的每个实例只能有一种序列化表示形式。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中对序列化字节执行比较操作时，其结果应与在托管代码中执行同样的比较操作时的结果相同。 当**IsByteOrdered**设置为**true**时，还支持以下功能：  
  
-   可以对此类型的列创建索引。  
  
-   可以对此类型的列创建主键和外键以及 CHECK 和 UNIQUE 约束。  
  
-   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 和 PARTITION BY 子句。 此时，将使用该类型的二进制表示形式确定顺序。  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用比较运算符。  
  
-   可以保持此类型的计算列。  
  
 请注意，当**IsByteOrdered**设置为**True**时，**本机**和**用户定制**的序列化格式均支持以下比较运算符：  
  
-   等于 (=)  
  
-   不等于 (!=)  
  
-   大于号 (>)  
  
-   小于号 (\<)  
  
-   大于或等于 (>=)  
  
-   小于或等于 (&lt;=)  
  
### <a name="implementing-nullability"></a>实现为 Null 性  
 除了正确指定程序集的属性外，类还必须支持为 Null 性。 加载到中的 Udt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 null 的，但为了使 UDT 能够识别 null 值，该类必须实现**INullable**接口。 有关如何在 UDT 中实现为空性的详细信息和示例，请参阅[编写用户定义类型的代码](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字符串转换  
 若要支持与 UDT 的字符串转换，必须在类中提供**Parse**方法和**ToString**方法。 **Parse**方法允许将字符串转换为 UDT。 它必须声明为**静态**（或在 Visual Basic 中**共享**），并采用**SqlTypes. SqlString**类型的参数。 有关如何实现**Parse**和**ToString**方法的详细信息和示例，请参阅[编写用户定义类型的代码](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 Udt 必须支持与**xml**数据类型的转换，方法是符合 xml 序列化约定。 **System.Xml。序列化**命名空间包含用于将对象序列化为 XML 格式文档或流的类。 您可以选择使用**IXmlSerializable**接口来实现**xml**序列化，该接口提供对 xml 序列化和反序列化的自定义格式设置。  
  
 除了执行从 UDT 到**xml**的显式转换以外，xml 序列化还可让你：  
  
-   在转换为**xml**数据类型后，在 UDT 实例的值上使用**Xquery** 。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具有本机 XML Web 服务的参数化查询和 Web 方法中使用 UDT。  
  
-   使用 UDT 可以接收 XML 数据的大容量加载。  
  
-   序列化包含具有 UDT 列的表的数据集。  
  
 UDT 在 FOR XML 查询中不序列化。 若要执行显示 Udt 的 XML 序列化的 FOR XML 查询，请在 SELECT 语句中将每个 UDT 列显式转换为**xml**数据类型。 还可以将列显式转换为**varbinary**、 **varchar**或**nvarchar**。  
  
## <a name="see-also"></a>另请参阅  
 [Creating a User-Defined Type（创建用户定义类型）](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
