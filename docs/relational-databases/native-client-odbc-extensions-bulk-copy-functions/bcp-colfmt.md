---
title: bcp_colfmt | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_colfmt
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fe615792733b5633bcfd9e8d64e48edb8a6d219
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2018
---
# <a name="bcpcolfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  指定用户文件中的数据的源或目标格式。 当使用作为源格式， **bcp_colfmt**指定用作中大容量复制到的数据源的现有数据文件的格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 当用作目标格式，将创建数据文件，使用使用指定的列格式**bcp_colfmt**。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 为大容量复制启用 ODBC 连接句柄。  
  
 *idxUserDataCol*  
 正在为其指定格式的用户数据文件中的列序号。 第一列为 1。  
  
 *eUserDataType*  
 用户文件中此列的数据类型。 如果不同于数据库表中的相应列的数据类型 (*idxServerColumn*)，如有可能大容量复制将转换数据。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]引入了对 SQLXML 和 SQLUDT 数据类型令牌中支持*eUserDataType*参数。  
  
 *EUserDataType*参数枚举通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据类型标记、 不 ODBC C 数据类型枚举器。 例如，可以使用特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的类型 SQLCHARACTER 来指定一个 ODBC 类型 SQL_C_CHAR 的字符串。  
  
 若要为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型指定默认的数据表示形式，则将此参数设置为 0。  
  
 有关大容量复制出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到文件，当*eUserDataType* SQLDECIMAL 或 SQLNUMERIC:  
  
-   如果源列不是**十进制**或**数值**，使用默认精度和小数位数。  
  
-   如果源列是**十进制**或**数值**，使用的精度和源列的小数位数。  
  
 *cbIndicator*  
 列数据中的长度/Null 指示器的长度（字节）。 有效指示器长度值是 0（不使用任何指示器时）、1、2、4 或 8。  
  
 若要指定默认的大容量复制指示器用法，请将此参数设置为 SQL_VARLEN_DATA。  
  
 指示器在内存中出现在任何数据的紧前面，在数据文件中出现在它们适用于的数据的紧前面。  
  
 如果使用多种方法来指定数据文件列长度（例如指示器和最大列长度，或者指示器和终止符序列），则大容量复制将选择导致数据复制量最少的方法。  
  
 如果列数据可能在长度上发生变化或列可能接受 NULL 作为值，则在没有调整数据格式的用户干预时，大容量复制生成的数据文件将包含指示器。  
  
 *cbUserData*  
 用户文件中该列数据的最大长度（字节），不包括任何长度指示器或终止符的长度。  
  
 设置*cbUserData*到 SQL_NULL_DATA 指示数据文件列中的所有值，或应设置为 NULL。  
  
 设置*cbUserData*于 SQL_VARLEN_DATA 会指示系统将确定每个列中的数据的长度。 对于某些列，这可能意味着生成长度/空指示符，以便置于来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的副本的数据前，或者意味着该指示符应位于复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据中。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符和二进制数据类型， *cbUserData*可以 SQL_VARLEN_DATA、 SQL_NULL_DATA，0，或某些正值。 如果*cbUserData*是 SQL_VARLEN_DATA，系统使用长度指示器，如果存在或终止符序列以确定数据的长度。 如果长度指示符和终止符序列均提供，则大容量复制将采用导致数据复制量最少的方法。 如果*cbUserData*是 SQL_VARLEN_DATA，数据类型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字符或二进制类型和一个长度指示符和终止符序列均未指定，系统将返回一条错误消息。  
  
 如果*cbUserData*为 0 或正值，系统使用*cbUserData*作为最大数据长度。 但是，如果是，除了一个正*cbUserData*、 提供长度指示器或终止符序列、 系统确定使用最少要复制的数据量会导致方法的数据长度。  
  
 *CbUserData*值表示的数据的字节数。 如果字符数据表示通过 Unicode 宽字符，则一个值为正*cbUserData*参数值表示乘以大小，以字节为单位，每个字符的字符数。  
  
 *pUserDataTerm*  
 要用于该列的终止符序列。 此参数主要用于字符数据类型，因为所有其他类型均属于固定长度，或者在二进制数据的情况下，要求长度指示器以精确记录提供的字节数目。  
  
 为了避免终止提取的数据，或者指示用户文件中的数据不终止，可将此参数设置为 NULL。  
  
 如果使用多种方法指定用户文件列长度（例如终止符和长度指示器，或者终止符和最大列长度），则大容量复制选择导致数据复制量最少的方法。  
  
 大容量复制 API 根据需要执行 Unicode 到 MBCS 的字符转换。 执行此操作时请务必小心，以便确保终止符字节字符串和字节字符串的长度都正确设置。  
  
 *cbUserDataTerm*  
 要用于该列的终止符序列的长度（字节）。 如果终止符不存在或不希望其出现在数据中，请将该值设置为 0。  
  
 *idxServerCol*  
 为数据库表中的列的序号位置。 第一个列编号为 1。 列的序号位置报告的[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
 如果该值是 0，则大容量复制将忽略数据文件中的该列。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>注释  
 **Bcp_colfmt**函数允许你指定大容量复制的用户文件格式。 对于大容量复制，格式包含以下部分：  
  
-   从用户文件列到数据库列的映射。  
  
-   每个用户文件列的数据类型。  
  
-   每个列的可选指示符的长度。  
  
-   每个用户文件列的数据的最大长度。  
  
-   每个列的可选终止字节序列。  
  
-   可选终止字节序列的长度。  
  
 每次调用**bcp_colfmt**指定某一用户文件列的格式。 例如，若要更改五列用户数据文件中的三个列的默认设置，请先调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**，然后调用**bcp_colfmt**五次，并在三个设置自定义格式这些调用。 对于剩余的两个调用，设置*eUserDataType*为 0，并集*cbIndicator*， *cbUserData*，和*cbUserDataTerm*为 0，SQL_VARLEN_DATA，和 0 分别。 此过程复制全部五列，其中的三列采用您的自定义格式，另两列采用默认格式。  
  
 有关*cbIndicator*，8，以指示较大的值类型的值现在是有效。 如果为其相应列是新的 max 类型的字段指定了前缀，则只能将它设置为 8。 有关详细信息，请参阅[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)。  
  
 **Bcp_columns**必须任何调用之前调用函数**bcp_colfmt**。  
  
 必须调用**bcp_colfmt**一次针对每个列中的用户文件。  
  
 调用**bcp_colfmt**不止一次的任何用户文件列会导致错误。  
  
 不需要将用户文件中的所有数据都复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 若要跳过列，指定的列，设置数据格式*idxServerCol*参数设为 0。 如果您要跳过某一列，则必须指定其类型。  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)函数可以用于持久保存的格式规范。  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>对增强的日期和时间功能的 bcp_colfmt 支持  
 有关与使用的类型信息*eUserDataType*参数对于日期/时间类型，请参阅[增强日期和时间类型 &#40;（OLE DB 和 ODBC）; 的大容量复制更改](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 有关详细信息，请参阅[日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
