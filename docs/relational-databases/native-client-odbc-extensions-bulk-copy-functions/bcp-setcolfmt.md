---
title: bcp_setcolfmt |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_setcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ad3993a22e0b2ec2091b0d37598f9cd6546d34aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32947782"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **Bcp_setcolfmt**函数取代[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。 在指定列的排序规则， **bcp_setcolfmt**必须使用函数。 [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)可用来指定多个列格式。  
  
 该函数提供在大容量复制操作中指定列格式的灵活方法。 它用于设置单独的列格式属性。 每次调用**bcp_setcolfmt**设置一个列格式属性。  
  
 **Bcp_setcolfmt**函数指定用户文件中的数据源或目标的格式。 当使用作为源格式， **bcp_setcolfmt**指定用作数据源中大容量复制到的表中的数据的现有数据文件的格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 当用作目标格式，将创建数据文件，使用使用指定的列格式**bcp_setcolfmt**。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_setcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbValue);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 field  
 要设置其属性的按一定顺序的列号。  
  
 *属性*  
 属性常量之一。 在下表中定义属性常量。  
  
|属性|“值”|Description|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|用户文件中此列的数据类型。 如果不同于数据库表中相应列的数据类型，则大容量复制将根据情况转换数据。<br /><br /> BCP_FMT_TYPE 参数由 sqlncli.h 中的 SQL Server 数据类型标记枚举，而非采用 ODBC C 数据类型枚举器。 例如，您可以使用特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 SQLCHARACTER 类型指定一个字符串：ODBC 类型 SQL_C_CHAR。<br /><br /> 若要为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型指定默认的数据表示形式，则将此参数设置为 0。<br /><br /> 用于为文件，请 BCP_FMT_TYPE 时 SQLDECIMAL 或 SQLNUMERIC，如果源列不是从 SQL Server 大容量复制**十进制**或**数值**，使用默认精度和小数位数。 否则为如果源列是**十进制**或**数值**，使用的精度和源列的小数位数。|  
|BCP_FMT_INDICATOR_LEN|INT|以字节表示的指示器（前缀）的长度。<br /><br /> 它是列数据中以字节表示的长度/空指示器的长度。 有效的指示器长度值是 0（在未使用指示器时）、1、2 或 4。<br /><br /> 若要指定默认的大容量复制指示器用法，请将此参数设置为 SQL_VARLEN_DATA。<br /><br /> 指示器在内存中出现在任何数据的紧前面，在数据文件中出现在它们适用于的数据的紧前面。<br /><br /> 如果使用多种方法来指定数据文件列长度（例如指示器和最大列长度，或者指示器和终止符序列），则大容量复制将选择导致数据复制量最少的方法。<br /><br /> 如果列数据可能在长度上发生变化或列可能接受 NULL 作为值，则在没有调整数据格式的用户干预时，大容量复制生成的数据文件将包含指示器。|  
|BCP_FMT_DATA_LEN|DBINT|用字节表示的数据的长度（列长度）。<br /><br /> 它是用户文件中此列的数据的用字节表示的最大长度，不包括任何长度指示器或终止符的长度。<br /><br /> 如果将 BCP_FMT_DATA_LEN 设置为 SQL_NULL_DATA，则指示数据文件列中的所有值均为或应该设置为 NULL。<br /><br /> 如果将 BCP_FMT_DATA_LEN 设置为 SQL_VARLEN_DATA，则指示系统应确定各列中数据的长度。 对于某些列，这可能意味着生成长度/空指示符，以便置于来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的副本的数据前，或者意味着该指示符应位于复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据中。<br /><br /> 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字符和二进制数据类型，BCP_FMT_DATA_LEN 可以是 SQL_VARLEN_DATA、SQL_NULL_DATA、0 或者某些正值。 如果 BCP_FMT_DATA_LEN 是 SQL_VARLEN_DATA，则系统将使用长度指示符（如果存在）或终止符序列，以便确定数据的长度。 如果长度指示符和终止符序列均提供，则大容量复制将采用导致数据复制量最少的方法。 如果 BCP_FMT_DATA_LEN 是 SQL_VARLEN_DATA，数据类型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字符或二进制类型，并且长度指示器和终止符序列均未指定，则系统将返回错误消息。<br /><br /> 如果 BCP_FMT_DATA_LEN 是 0 或正值，则系统使用 BCP_FMT_DATA_LEN 作为最大数据长度。 但是，如果除了正的 BCP_FMT_DATA_LEN 外，还提供了长度指示器或终止符序列，则系统将通过使用导致数据复制量最少的方法，确定数据长度。<br /><br /> BCP_FMT_DATA_LEN 值表示数据的字节计数。 如果字符数据由 Unicode 宽字符表示，则正的 BCP_FMT_DATA_LEN 参数值表示字符数目乘以每个字符的大小（用字节表示）。|  
|BCP_FMT_TERMINATOR|LPCBYTE|指向要用于此列的终止符序列（相应为 ANSI 或 Unicode）的指针。 此参数主要用于字符数据类型，因为所有其他类型均属于固定长度，或者在二进制数据的情况下，要求长度指示器以精确记录提供的字节数目。<br /><br /> 为了避免终止提取的数据，或者指示用户文件中的数据不终止，可将此参数设置为 NULL。<br /><br /> 如果使用多种方法指定用户文件列长度（例如终止符和长度指示器，或者终止符和最大列长度），则大容量复制选择导致数据复制量最少的方法。<br /><br /> 大容量复制 API 根据需要执行 Unicode 到 MBCS 的字符转换。 执行此操作时请务必小心，以便确保终止符字节字符串和字节字符串的长度都正确设置。|  
|BCP_FMT_SERVER_COL|INT|数据库中列的序号位置|  
|BCP_FMT_COLLATION|LPCSTR|排序规则名。|  
  
 *pValue*  
 是一个指针指向要关联到的值*属性*。 它允许单独设置每个列格式属性。  
  
 *cbvalue*  
 以字节表示的属性缓冲区的长度。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 此函数将取代**bcp_colfmt**函数。 所有功能**bcp_colfmt**中提供**bcp_setcolfmt**函数。 此外，还提供对列排序规则的支持。 建议按照下面给出的顺序设置以下列格式属性：  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 **Bcp_setcolfmt**函数允许你指定大容量复制的用户文件格式。 对于大容量复制，格式包含以下部分：  
  
-   从用户文件列到数据库列的映射。  
  
-   每个用户文件列的数据类型。  
  
-   每个列的可选指示符的长度。  
  
-   每个用户文件列的数据的最大长度。  
  
-   每个列的可选终止字节序列。  
  
-   可选终止字节序列的长度。  
  
 每次调用**bcp_setcolfmt**指定某一用户文件列的格式。 例如，若要更改五列用户数据文件中的三个列的默认设置，请先调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**，然后调用**bcp_setcolfmt**五次，有三个设置自定义格式这些调用。 对于剩余的两个调用，BCP_FMT_TYPE 设置为 0，并设置 BCP_FMT_INDICATOR_LENGTH，BCP_FMT_DATA_LEN，和*cbValue*为 0，SQL_VARLEN_DATA，和 0 分别。 此过程复制全部五列，其中的三列采用您的自定义格式，另两列采用默认格式。  
  
 **Bcp_columns**必须在调用之前调用函数**bcp_setcolfmt**。  
  
 必须调用**bcp_setcolfmt**一次针对每个列中的用户文件的每个属性。  
  
 您不需要将用户文件中的所有数据都复制到 SQL Server 表中。 若要跳过某一列，请指定该列的数据格式，并且将 BCP_FMT_SERVER_COL 参数设置为 0。 如果您要跳过某一列，则必须指定其类型。  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)函数可以用于持久保存的格式规范。  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>针对增强的日期和时间功能的 bcp_setcolfmt 支持  
 与 BCP_FMT_TYPE 属性用于日期/时间类型的类型是作为中指定[增强日期和时间类型的大容量复制更改&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
