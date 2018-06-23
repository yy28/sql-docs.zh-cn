---
title: IBCPSession::BCPControl (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPControl (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPControl method
ms.assetid: d58f3fe1-45e3-4e46-8e9c-000971829d99
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8fe87c59b16467462891fe914cdba31bf9c1af4a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137517"
---
# <a name="ibcpsessionbcpcontrol-ole-db"></a>IBCPSession::BCPControl (OLE DB)
  设置大容量复制操作的选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT BCPControl(   
inteOption,  
void *iValue);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPControl**方法会设置进行大容量复制操作包括在取消大容量复制，要将一个数据文件和批大小从复制的第一个和最后一个行的数字之前允许的错误数的各种控制参数。  
  
 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大容量复制数据时，此方法还可用于指定要使用的 SELECT 语句。 你可以设置`eOption`BCP_OPTION_HINTS 自变量和`iValue`要有一个指针指向包含 SELECT 语句的宽字符字符串自变量。  
  
 可能的值有*eOption*是：  
  
|选项|Description|  
|------------|-----------------|  
|BCP_OPTION_ABORT|停止正在进行的大容量复制操作。 你可以调用**BCPControl**方法替换*eOption*的 BCP_OPTION_ABORT 从另一个线程来停止正在运行的大容量复制操作的自变量。 *IValue*忽略自变量。|  
|BCP_OPTION_BATCH|每批的行数。 默认值为 0，提取数据时，该值指示表中的所有行，或用户数据中的所有行都文件时正在将数据复制到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 值小于 1 则将 BCP_OPTION_BATCH 重置为默认值。|  
|BCP_OPTION_DELAYREADFMT|布尔值，如果设置为 true，将导致[IBCPSession::BCPReadFmt](ibcpsession-bcpreadfmt-ole-db.md)读取在执行。 如果为 false （默认值），IBCPSession::BCPReadFmt 立即将读取格式化文件。 如果将发生序列错误`BCP_OPTION_DELAYREADFMT`是 true，并且您调用 IBCPSession::BCPColumns 或 IBCPSession::BCPColFmt。<br /><br /> 如果调用，也会出现序列错误`IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)FALSE))`之后调用`IBCPSession::BCPControl(BCPDELAYREADFMT, (void *)TRUE)`和 IBCPSession::BCPWriteFmt。<br /><br /> 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。|  
|BCP_OPTION_FILECP|*IValue*自变量包含数据文件的代码页的数目。 可以指定代码页的编号，例如 1252 或 850，或者采用以下值之一：<br /><br /> -BCP_FILECP_ACP： 文件中的数据是在客户端的 Microsoft Windows® 代码页。<br />-BCP_FILECP_OEMCP： 文件中的数据是在客户端 （默认值） 的 OEM 代码页。<br />-BCP_FILECP_RAW： 文件中的数据是中的代码页[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|BCP_OPTION_FILEFMT|数据文件格式的版本号。 该版本号可以是 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)])、90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)])、100（[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]）、110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 或 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 120 是默认值。 对于采用服务器早期版本所支持的格式的数据，该选项对导出和导入这样的数据非常有用。  例如，若要将数据导入从获取文本列中[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]服务器成为**varchar （max)** 中的列[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本的服务器，你应指定 80。 同样，如果在将数据从导出时指定 80 **varchar （max)** 列，则会保存图像一样文本列保存在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]格式化，并可以导入到的文本列[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]服务器。|  
|BCP_OPTION_FIRST|文件或表要复制的数据的第一行。 默认值为 1；值小于 1 则将此选项重置为其默认值。|  
|BCP_OPTION_FIRSTEX|对于 BCP out 操作，指定要复制到数据文件的数据库表的第一行。<br /><br /> 对于 BCP in 操作，指定要复制到数据库表的数据文件的第一行。<br /><br /> *IValue*参数应为一个有符号的 64 位整数，它包含的值的地址。 可以传递到 BCPFIRSTEX 的最大值为 2^63-1。|  
|BCP_OPTION_FMTXML|用于指定生成的格式化文件应采用 XML 格式。 默认情况下关闭此选项，此时将格式化文件作为文本文件保存。 XML 格式化文件提供更大的灵活性，但具有某些额外约束。 例如，不能同时为字段指定前缀和终止符，而在较早的格式化文件中则可以执行此操作。 **注意：** XML 格式化文件才支持时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起安装工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。|  
|BCP_OPTION_HINTS|*IValue*自变量包含的宽字符字符串指针。 寻址的字符串指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大容量复制处理提示或返回结果集的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 如果指定返回多个结果集的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，则忽略第一个结果集之后的所有结果集。|  
|BCP_OPTION_KEEPIDENTITY|当*iValue*自变量设置为 TRUE，则此选项指定的大容量复制方法插入为提供的数据值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 identity 约束定义的列。 输入文件必须提供标识列的值。 如果未进行设置，则为插入的行生成新标识值。 忽略文件的标识列中所存在的任何数据。|  
|BCP_OPTION_KEEPNULLS|指定是否会将文件中的空数据值转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的 NULL 值。 当*iValue*参数设置为 TRUE，空值将转换为中的 NULL[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 默认情况下会将空值转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的列的默认值（如果存在默认值）。|  
|BCP_OPTION_LAST|要复制的最后一行。 默认值为复制所有行。 值小于 1 则将此选项重置为其默认值。|  
|BCP_OPTION_LASTEX|对于 BCP out 操作，指定要复制到数据文件的数据库表的最后一行。<br /><br /> 对于 BCP in 操作，指定要复制到数据库表的数据文件的最后一行。<br /><br /> *IValue*参数应为一个有符号的 64 位整数，它包含的值的地址。 可以传递到 BCPLASTEX 的最大值为 2^63-1。|  
|BCP_OPTION_MAXERRS|在大容量复制操作失败之前允许的错误数。 默认值为 10。 值小于 1 则将此选项重置为其默认值。 大容量复制将最大错误数限制为 65,535 个。 如果尝试将该选项设置为大于 65,535 的值，将导致该选项设置为 65,535。|  
|BCP_OPTION_ROWCOUNT|返回当前（或上一次）BCP 操作所影响的行数。|  
|BCP_OPTION_TEXTFILE|数据文件不是二进制文件而是文本文件。 BCP 将通过检查数据文件的前两个字节中的 Unicode 字节标记来确定该文本文件是否是 Unicode。|  
|BCP_OPTION_UNICODEFILE|如果设置为 TRUE，则此选项指定输入文件是 Unicode 文件格式。|  
  
## <a name="arguments"></a>参数  
 *eOption*[in]  
 设置为以上备注一节中所列的选项之一。  
  
 *iValue*[in]  
 指定的值*eOption*。 *IValue*自变量是强制转换为 void 的指针，以便将来扩展为 64 位值的整数值。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_FAIL  
 提供程序特定出错;详细信息，请使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)接口。  
  
 E_UNEXPECTED  
 意外调用了该方法。 例如， [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md)方法未调用此函数之前调用。  
  
 E_OUTOFMEMORY  
 内存不足错误。  
  
## <a name="see-also"></a>请参阅  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)  
  
  