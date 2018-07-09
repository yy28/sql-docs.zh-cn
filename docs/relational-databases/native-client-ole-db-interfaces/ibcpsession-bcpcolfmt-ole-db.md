---
title: 'Ibcpsession:: Bcpcolfmt (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPColFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColFmt method
ms.assetid: 2852f4ba-f1c6-4c4c-86b2-b77e4abe70de
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e11dc5983421ce89cf29131212c2d193fda20326
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432536"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在程序变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 列之间创建绑定。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPColFmt(   
      DBORDINAL idxUserDataCol,  
      int eUserDataType,  
      int cbIndicator,  
      int cbUserData,  
      BYTE *pbUserDataTerm,  
      int cbUserDataTerm,  
      DBORDINAL idxServerCol);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPColFmt**方法用于创建 BCP 数据文件字段之间的绑定和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列。 它将列的长度、类型、终止符和前缀长度视为参数处理，并为各个字段设置所有这些属性。  
  
 如果用户选择交互模式，则调用该方法两次；一次按照默认值（与服务器列的类型相对应）设置列格式，另一次按照在交互模式期间选择的客户端的所选列类型为每个列设置格式。  
  
 在非交互模式中，对每列只调用它一次，以便将每个列的类型设置为字符或本机类型，并设置列和行终止符。  
  
 **BCPColFmt**方法，可指定大容量复制的用户文件格式。 对于大容量复制，格式包含以下部分：  
  
-   从用户文件字段到数据库列的映射。  
  
-   每个用户文件字段的数据类型。  
  
-   每个字段的可选指示器的长度。  
  
-   每个用户文件字段中数据的最大长度。  
  
-   每个字段的可选终止字节序列。  
  
-   可选终止字节序列的长度。  
  
 每次调用**BCPColFmt**指定一个用户文件字段的格式。 例如，若要更改在五个字段的用户数据文件中的三个字段的默认设置，请先调用`BCPColumns(5)`，然后调用**BCPColFmt**五次，其中三次调用设置您的自定义格式。 对于剩余的两个调用，设置*eUserDataType*为 BCP_TYPE_DEFAULT，并将*cbIndicator*， *cbUserData*，和*cbUserDataTerm*为 0、bcp_variable_length 和 0 分别。 此过程复制全部五列，其中的三列采用您的自定义格式，另两列采用默认格式。  
  
> [!NOTE]  
>  [Ibcpsession:: Bcpcolumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)到进行任何调用之前，必须在调用方法**BCPColFmt**。 必须调用**BCPColFmt**一次针对每个用户文件中的列。 调用**BCPColFmt**不止一次对任何用户文件列会导致错误。  
  
 不必将用户文件中的所有数据复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 若要跳过某一列，请指定该列的数据格式，并且将 idxServerCol 参数设置为 0。 若要跳过某一字段，仍然需要所有信息才能让该方法正常工作。  
  
 **请注意** [ibcpsession:: Bcpwritefmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)函数可用于维持格式规范通过提供**BCPColFmt**。  
  
## <a name="arguments"></a>参数  
 *idxUserDataCol*[in]  
 用户的数据文件中字段的索引。  
  
 *eUserDataType*[in]  
 用户的数据文件中字段的数据类型。 中列出可用的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 头文件 (sqlncli.h) 以 BCP_TYPE_XXX 格式，例如，BCP_TYPE_SQLINT4。 如果指定 BCP_TYPE_DEFAULT 值，则访问接口将尝试使用与表或视图列相同的类型。 大容量复制操作，共[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到一个文件时**eUserDataType**参数是 BCP_TYPE_SQLDECIMAL 或 BCP_TYPE_SQLNUMERIC:  
  
-   如果源列的数据类型不是 decimal 或 numeric，则使用默认的精度和小数位数。  
  
-   如果源列的数据类型是 decimal 或 numeric，则使用源列的精度和小数位数。  
  
 *cbIndicator*[in]  
 字段的前缀长度。 默认是 BCP_PREFIX_DEFAULT。 前缀的有效长度是 0、1、2、4 和 8。 大多数情况下，使用等于 8 的前缀大小指示字段已块区化。 这用于有效地大容量复制大型值类型列。  
  
 *cbUserData*[in]  
 用户文件中该字段的数据的最大长度（单位为字节），不包括任何长度指示器或终止符的长度。  
  
 设置**cbUserData**为 BCP_LENGTH_NULL 指示文件字段的数据中的所有值，或是否应设置为 NULL。 设置**cbUserData**为 bcp_length_variable，则指示系统应当确定每个字段的数据的长度。 对于某些字段，这可能意味着将生成长度/Null 指示器，并将该指示器放在从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的数据的前面，或者应当将该指示器放在复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据中。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符和二进制数据类型**cbUserData**可以是 BCP_LENGTH_VARIABLE，BCP_LENGTH_NULL，0，或某个正值。 如果**cbUserData**是 BCP_LENGTH_VARIABLE，则系统使用长度指示符，如果存在或终止符序列来确定数据的长度。 如果长度指示符和终止符序列均提供，则大容量复制将采用导致数据复制量最少的方法。 如果**cbUserData**是 bcp_length_variable，而且数据类型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符或二进制类型，然后如果长度指示器和终止符序列均未指定，系统将返回一条错误消息。  
  
 如果**cbUserData**为 0 或正值，则系统使用**cbUserData**作为最大数据长度。 但是，如果除了正**cbUserData**、 提供长度指示器或终止符序列，系统使用导致数据复制量最少的方法来确定数据长度。  
  
 **CbUserData**值表示数据的字节计数。 如果字符数据由 Unicode 宽字符，则正**cbUserData**参数值表示乘以大小，以字节为单位，每个字符的字符数。  
  
 *pbUserDataTerm*[size_is][in]  
 用于字段的终止符序列。 此参数主要用于字符数据类型，因为所有其他类型均属于固定长度，或者在二进制数据的情况下，要求长度指示器以精确记录提供的字节数目。  
  
 为了避免终止提取的数据，或者指示用户文件中的数据不终止，可将此参数设置为 NULL。  
  
 如果使用多种方法指定用户文件列长度（例如终止符和长度指示器，或者终止符和最大列长度），则大容量复制选择导致数据复制量最少的方法。  
  
 大容量复制 API 根据需要执行 Unicode 到 MBCS 的字符转换。 执行此操作时请务必小心，以便确保终止符字节字符串和字节字符串的长度都正确设置。  
  
 *cbUserDataTerm*[in]  
 要用于列的终止符序列的长度（单位为字节）。 如果终止符不存在或不希望其出现在数据中，请将该值设置为 0。  
  
 *idxServerCol*[in]  
 数据库表中列的序号位置。 第一个列编号为 1。 报告列的序号位置**icolumnsinfo:: Getcolumninfo**或类似的方法。 如果该值是 0，则大容量复制将忽略数据文件中的相应字段。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 有关详细的信息可使用提供程序特定错误发生[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， [ibcpsession:: Bcpinit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)调用此方法之前，未调用方法。  
  
 E_INVALIDARG  
 参数无效。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [执行大容量复制操作](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
