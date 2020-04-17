---
title: 用户定义的类型要求 |微软文档
description: 本文介绍了在创建要在 SQL Server 上安装的 UDT 时需要做出的重要设计决策。
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
ms.openlocfilehash: 2b19a9179cba2225a2209255ce48220669e4bbef
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486966"
---
# <a name="creating-user-defined-types---requirements"></a>创建用户定义类型 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在创建要安装在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的用户定义类型 （UDT） 时，必须做出几个重要的设计决策。 对于大多数 UDT，建议将 UDT 作为结构创建，尽管也可以选择将其作为类创建。 UDT 定义必须符合用于创建 UDT 的规范，以使其能够注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="requirements-for-implementing-udts"></a>实现 UDT 的要求  
 为了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行，您的 UDT 必须实现 UDT 定义中的以下要求：  
  
 UDT 必须指定**Microsoft.SqlServer.Server.SqlUser 定义类型属性**。 系统.**可序列化属性**的使用是可选的，但建议使用。  
  
-   UDT 必须通过创建公共**静态**（在可视基本中[!INCLUDE[msCoName](../../includes/msconame-md.md)]**共享****）Null**方法在类或结构中实现**System.Data.SqlType.INull 接口**。 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 Null 的。 这是为使在 UDT 中执行的代码能够识别 Null 值所必需的。  
  
-   UDT 必须包含支持从中解析的公共**静态**（或**共享**）**解析**方法，以及用于转换为对象的字符串表示形式的公共**ToString**方法。  
  
-   具有用户定义的序列化格式的 UDT 必须实现**System.Data.IBinary 序列化**接口并提供**读取**和**写入**方法。  
  
-   UDT 必须实现**System.Xml.序列化.IXml 序列化**，或者所有公共字段和属性必须是 XML 可序列化或使用**XmlIgnore**属性修饰的类型（如果需要重写标准序列化）。  
  
-   一个 UDT 对象必须只存在一个序列化。 如果序列化或反序列化例程识别了某一特定对象的多个表示形式，则验证将失败。  
  
-   **SqlUser 定义类型属性.IsByteOrder**必须**为 true，** 才能按字节顺序比较数据。 如果未实现 I可比较接口，并且**SqlUser 定义Typeattribute.IsByteOrderafalse，** 字节顺序比较将失败。 **false**  
  
-   在类中定义的 UDT 必须具有不采用任何参数的公共构造函数。 您可以选择创建其他重载类构造函数。  
  
-   该 UDT 必须将数据元素作为公共字段或属性过程公开。  
  
-   公共名称不能超过 128 个字符，并且必须符合[数据库标识符](../../relational-databases/databases/database-identifiers.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定义的标识符的命名规则。  
  
-   **sql_variant**列不能包含 UDT 的实例。  
  
-   继承的成员无法从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统不知道 UDT 中的继承层次结构。 但是，您可以在创建类的结构时使用继承，并且可以在该类型的托管代码实现方式中调用此类方法。  
  
-   成员不能被重载，但类构造函数除外。 如果您创建某一重载方法，则在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集或创建类型时将不会引发错误。 在运行时将检测到重载的方法，而不是在创建类型时检测到。 只要永不调用重载的方法，重载的方法就可以存在于类中。 一旦您调用重载的方法，就会引发错误。  
  
-   任何**静态**（或**共享**）成员都必须声明为常量或只读。 静态成员将无法改变。  
  
-   如果**SqlUser 定义TypeAttribute.MaxByteSize**字段设置为 -1，则序列化 UDT 可以大到大对象 （LOB） 大小限制（目前为 2 GB）。 UDT 的大小不能超过**MaxByteSize**字段中指定的值。  
  
> [!NOTE]  
>  尽管服务器不使用它执行比较，但您可以选择实现**System.IThecomp 接口**，该接口公开单个方法**比较。** 此方法用于客户端上希望精确比较或排序 UDT 值的情况中。  
  
## <a name="native-serialization"></a>本机序列化  
 为您的 UDT 选择正确的序列化属性取决于您正尝试创建的 UDT 的类型。 **本机**序列化格式使用非常简单的结构，能够在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]磁盘上存储 UDT 的有效本机表示形式。 如果 UDT 简单且仅包含以下类型的字段，则建议使用**本机**格式：  
  
 **布尔**，**字节**，**字节**，**短**， **ushort，** **int，** **uint，****长**，**乌龙**，**浮动**，**双**， **SqlByte，** **SqlInt16，** **SqlInt32，** **SqlInt64，** **SqlDatetime，** **SqlSingle，** **SqlDouble，** **SqlMoney，** **SqlBoolean**  
  
 由上述类型的字段组成的值类型是**本机**格式的良好候选项，例如 Visual C# 中的**结构**（或 Visual Basic 中已知的**结构**）。 例如，使用**本机**序列化格式指定的 UDT 可能包含另一个 UDT 的字段，该字段也使用**本机**格式指定。 如果 UDT 定义更为复杂，并且包含不在上述列表中的数据类型，则必须改为指定 User**定义**序列化格式。  
  
 **本机**格式具有以下要求：  
  
-   该类型不得为**Microsoft.SqlServer.Server.Server.SqlUser 定义类型属性指定值**。  
  
-   所有字段必须均可序列化。  
  
-   如果 UDT 是在类中定义的，而不是结构中定义的，则必须将**系统.Runtime.InteropServices.StructLayout属性**指定为 **"结构布局"。LayoutKind顺序**。 此属性控制数据字段的物理布局，并用来按照成员的出现顺序对它们进行布局。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此属性确定具有多个值的 UDT 的字段顺序。  
  
 有关使用**本机**序列化定义的 UDT 的示例，请参阅[编码用户定义类型的](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)点 UDT。  
  
## <a name="userdefined-serialization"></a>UserDefined 序列化  
 **Microsoft.SqlServer.Server.Server.SqlUser 定义类型属性**的用户**定义**格式设置使开发人员能够完全控制二进制格式。 将**Format**属性属性指定为 **"用户定义**"时，必须在代码中执行以下操作：  
  
-   指定可选的**IsByte顺序**属性属性。 默认值是 **false**秒。  
  
-   指定**Microsoft.SqlServer.Server.Server.SqlUser 定义类型属性**的**MaxByteSize**属性。  
  
-   通过实现**系统.Data.Sql.IBinary 序列化接口**编写代码以实现 UDT 的**读写**方法。 **Read**  
  
 有关使用**用户定义**序列化定义的 UDT 的示例，请参阅[编码用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)中的货币 UDT。  
  
> [!NOTE]  
>  为了编制索引，UDT 字段必须使用本机序列化或者是持久化的。  
  
## <a name="serialization-attributes"></a>序列化属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。 创建 UDT 时，您需要指定**Microsoft.SqlServer.Server.SqlUser 定义类型属性**。 **Microsoft.SqlServer.Server.SqlUser 定义类型属性属性**指示该类是 UDT 并指定 UDT 的存储。 您可以选择指定**可序列化**属性，尽管[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不需要这样做。  
  
 **Microsoft.SqlServer.Server.SqlUser 定义类型属性**具有以下属性。  
  
 **格式**  
 指定序列化格式（可以是**本机**格式或**用户定义**格式，具体取决于 UDT 的数据类型）。  
  
 **IsByteOrdered**  
 确定**Boolean**如何在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UDT 上执行二进制比较的布尔值。  
  
 **IsFixedLength**  
 指示此 UDT 的所有实例是否都具有相同的长度。  
  
 **MaxByteSize**  
 实例的最大大小（以字节为单位）。 您必须使用**用户定义的**序列化格式指定**MaxByteSize。** 对于指定用户定义的序列化的**UDT，MaxByteSize**是指用户定义的序列化形式的 UDT 的总大小。 **MaxByteSize**的值必须在 1 到 8000 的范围内，或设置为 -1 以指示 UDT 大于 8000 字节（总大小不能超过最大 LOB 大小）。 考虑一个包含 10 个字符字符串属性 （**System.Char**） 的 UDT。 当使用 BinaryWriter 序列化 UDT 时，序列化字符串的总大小为 22 字节：每个 Unicode UTF-16 字符占 2 个字节，乘以最大字符数，再加上因序列化二进制流而导致的系统开销 2 个控制字节。 因此，在确定**MaxByteSize**的值时，必须考虑序列化 UDT 的总大小：以二进制形式序列化的数据的大小加上序列化产生的开销。  
  
 **验证方法名称**  
 用于验证 UDT 的实例的方法的名称。  
  
### <a name="setting-isbyteordered"></a>设置 IsByteOrdered  
 当**Microsoft.SqlServer.Server.Server.SqlUser定义Typeattribute.IsByteOrdered**属性设置为**true**时，您实际上保证序列化二进制数据可用于信息的语义排序。 因此，以字节排序的 UDT 对象的每个实例只能有一种序列化表示形式。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中对序列化字节执行比较操作时，其结果应与在托管代码中执行同样的比较操作时的结果相同。 当**IsByteOrdered**设置为**true**时，还支持以下功能：  
  
-   可以对此类型的列创建索引。  
  
-   可以对此类型的列创建主键和外键以及 CHECK 和 UNIQUE 约束。  
  
-   可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY、GROUP BY 和 PARTITION BY 子句。 此时，将使用该类型的二进制表示形式确定顺序。  
  
-   可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用比较运算符。  
  
-   可以保持此类型的计算列。  
  
 请注意，当**IsByteOrdered**设置为**true**时，**本机**和**用户定义的**序列化格式都支持以下比较运算符：  
  
-   等于 (=)  
  
-   不等于 (!=)  
  
-   大于号 (>)  
  
-   小于号 (\<)  
  
-   大于或等于 (>=)  
  
-   小于或等于 (&lt;=)  
  
### <a name="implementing-nullability"></a>实现为 Null 性  
 除了正确指定程序集的属性外，类还必须支持为 Null 性。 加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 UDT 是 null 感知的，但为了 UDT 识别 null 值，类必须实现**INull 可接口**。 有关详细信息以及如何在 UDT 中实现 null 的的示例，请参阅[编写用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
### <a name="string-conversions"></a>字符串转换  
 要支持与 UDT 的字符串转换，必须在类中提供**分析**方法和**ToString**方法。 **解析**方法允许将字符串转换为 UDT。 它必须声明为**静态**（或在可视基本中**共享**），并采用**类型系统.Data.SqlType.SqlString 的**参数。 有关详细信息以及如何实现**分析**和**ToString**方法的示例，请参阅[编写用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)。  
  
## <a name="xml-serialization"></a>XML 序列化  
 UDT 必须支持通过遵循 XML 序列化协定来支持与**xml**数据类型转换。 **System.Xml.序列化**命名空间包含用于将对象序列化为 XML 格式文档或流的类。 您可以选择使用**IXml 序列化**接口实现**xml**序列化，该接口为 XML 序列化和反序列化提供自定义格式。  
  
 除了执行从 UDT 到**xml**的显式转换外，XML 序列化还使您能够：  
  
-   转换为**xml**数据类型后，对 UDT 实例的值使用**Xquery。**  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具有本机 XML Web 服务的参数化查询和 Web 方法中使用 UDT。  
  
-   使用 UDT 可以接收 XML 数据的大容量加载。  
  
-   序列化包含具有 UDT 列的表的数据集。  
  
 UDT 在 FOR XML 查询中不序列化。 要执行显示 UDT 的 XML 序列化的 FOR XML 查询，请显式将每个 UDT 列转换为 SELECT 语句中的**xml**数据类型。 您还可以显式将列转换为**varbinary、varchar****varchar**或**nvarchar**。  
  
## <a name="see-also"></a>另请参阅  
 [Creating a User-Defined Type（创建用户定义类型）](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
