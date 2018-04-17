---
title: IBCPSession::BCPInit (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPInit (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPInit method
ms.assetid: 583096d7-da34-49be-87fd-31210aac81aa
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 57ef664eebefaab57c45fa7a487b5af7fc84277f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="ibcpsessionbcpinit-ole-db"></a>IBCPSession::BCPInit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  初始化大容量复制结构，执行某些错误检查，验证数据和格式化文件名是否正确，然后打开文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPInit(   
      const wchar_t *pwszTable,  
      const wchar_t *pwszDataFile,  
      const wchar_t *pwszErrorFile,  
      int eDirection);  
```  
  
## <a name="remarks"></a>注释  
 **BCPInit**应该在大容量复制的任何其他方法之前调用方法。 **BCPInit**方法用于大容量复制工作站之间的数据执行必要的初始化和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **BCPInit**方法检查数据库源或目标表，不是数据文件的结构。 该方法将基于数据库表、视图或 SELECT 结果集中的每一列为数据文件指定数据格式值。 此指定包括每一列的数据类型、数据中是否存在长度或 Null 指示符和终止符字节字符串以及固定长度的数据类型的宽度。 **BCPInit**方法设置这些值，如下所示：  
  
-   指定的数据类型是数据库表、视图或 SELECT 结果集中的列的数据类型。 数据类型枚举通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的本机数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端标头文件 (sqlncli.h)。 数据类型的值为 BCP_TYPE_XXX 模式。 数据将以其计算机形式表示。 也就是说，整数数据类型的列中的数据通过一个由四个字节组成的序列表示，该序列采用 big-endian 或 little-endian 格式，具体使用哪种格式取决于创建该数据文件的计算机。  
  
-   如果数据库数据类型的长度是固定的，则该数据文件中的数据长度也是固定的。 处理数据的大容量复制方法 (例如， [IBCPSession::BCPExec](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)) 分析数据行应为要与数据库表、 视图或选择的列中指定的数据的长度相同的数据文件中的数据的长度列表。 例如，对于定义为 `char(13)` 的数据库列的数据，该文件中每行数据必须由 13 个字符来表示。 如果数据库列允许 Null 值，则可以使用 Null 指示符作为固定长度的数据的前缀。  
  
-   向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制数据时，数据文件必须包含数据库表中的每列数据。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制数据时，数据库表、视图或 SELECT 结果集中所有列的数据均将复制到数据文件。  
  
-   向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制数据时，数据文件中列的序号位置必须与数据库表中列的序号位置相同。 将数据从复制时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 **BCPExec**方法会将放在数据库表中的列的序号位置上基于的数据。  
  
-   如果数据库数据类型的长度是可变的（如 `varbinary(22)`），或者如果数据库列可以包含 Null 值，则在数据文件中使用长度/Null 指示符作为数据的前缀。 指示符的宽度因数据类型和大容量复制的版本而异。 [IBCPSession::BCPControl](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)方法选项 BCP_OPTION_FILEFMT 提供早期的大容量复制数据文件和运行更高版本的服务器之间的兼容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过指示何时中指示器的宽度数据是比预期更窄。  
  
> [!NOTE]  
>  若要更改为数据文件指定的数据格式值，使用[IBCPSession::BCPColumns](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)和[IBCPSession::BCPColFmt](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)方法。  
  
 大容量复制到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以通过设置数据库选项不包含索引的表的优化**选择到 / bulkcopy**。  
  
## <a name="arguments"></a>参数  
 *pwszTable*[in]  
 要复制进或复制出的数据库表的名称。 该名称可以包含数据库名称或所有者名称。 例如，"pubs.username.titles"、"pubs..titles"、"username.titles"。  
  
 如果 eDirection 参数设置为 BCP_DIRECTION_OUT，则 pwszTable 参数可以为数据库视图的名称。  
  
 如果 eDirection 参数设置为 BCP_DIRECTION_OUT 和使用指定的 SELECT 语句**BCPControl**方法，然后才能**BCPExec**调用方法时， *pwszTable*参数必须设置为 NULL。  
  
 *pwszDataFile*[in]  
 要复制进或复制出的用户文件的名称。  
  
 *pwszErrorFile*[in]  
 错误文件的名称，该文件将用进度消息、错误消息以及无法从用户文件复制到表的任何行的副本进行填充。 如果*pwszErrorFile*参数设置为 NULL，则使用任何文件时出错。  
  
 *eDirection*[in]  
 复制操作的方向，BCP_DIRECTION_IN 或 BCP_DIRECTION _OUT。 BCP_DIRECTION _IN 指示从用户文件向数据库表进行复制；BCP_DIRECTION _OUT 指示从数据库表向用户文件进行复制。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 提供程序特定错误的发生详细信息，请使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)接口。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
 E_INVALIDARG  
 未正确指定一个或多个参数。 例如，给定的文件名无效。  
  
## <a name="see-also"></a>另请参阅  
 [IBCPSession &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [执行大容量复制操作](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
