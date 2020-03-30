---
title: 适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持
ms.custom: ''
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: reference
ms.reviewer: v-kaywon
ms.author: jroth
author: rothja
ms.openlocfilehash: 340c1bdd7ab3ff54ffab52aebe08eeab258c7b41
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257688"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server（版本 18.2.1）添加了对 UTF-8 服务器编码的支持。 有关 SQL Server UTF-8 支持的信息，请参阅：
- [排序规则和 Unicode 支持](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 支持](#ctp23)

> [!IMPORTANT]
> Microsoft OLE DB Driver for SQL Server 使用 [GetACP](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp) 函数确定 DBTYPE_STR 输入缓冲区的编码。 不支持 GetACP 返回 UTF-8 编码的情况。 如果缓冲区需要存储 Unicode 数据，则应将缓冲区数据类型设置为 DBTYPE_WSTR（UTF-16 编码）。

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>将数据插入到 UTF-8 编码的 CHAR 或 VARCHAR 列中
创建输入参数缓冲区以便进行插入时，使用 [DBBINDING 结构](https://go.microsoft.com/fwlink/?linkid=2071182)的数组描述缓冲区。 每个 DBBINDING 结构将单个参数与使用者的缓冲区关联，并包含数据值的长度和类型等信息。 对于类型 CHAR 的输入参数缓冲区，DBBINDING 结构的 wType  应设置为 DBTYPE_STR。 对于类型 WCHAR 的输入参数缓冲区，DBBINDING 结构的 wType  应设置为 DBTYPE_WSTR。

执行包含参数的命令时，驱动程序将构造参数数据类型信息。 如果输入缓冲区类型与参数数据类型匹配，则不会在驱动程序中进行任何转换。 否则，驱动程序会将输入参数缓冲区转换为参数数据类型。 用户可以通过调用 [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577) 来显式设置参数数据类型。 如果未提供信息，则驱动程序会通过以下方式派生参数数据类型信息：(a) 当语句准备好后，从服务器中检索列元数据，或 (b) 尝试从输入参数数据类型进行默认转换。

输入参数缓冲区可以由驱动程序或服务器转换为服务器列排序规则，具体取决于输入缓冲区数据类型和参数数据类型。 在转换期间，如果客户端代码页或数据库排序规则代码页不能代表输入缓冲区中的所有字符，则可能会发生数据丢失。 下表介绍了将数据插入到启用了 UTF-8 的列中时的转换过程：

|缓冲区数据类型|参数数据类型|转换|用户预防措施|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|服务器从客户端代码页转换为数据库排序规则代码页；服务器从数据库排序规则代码页转换为列排序规则代码页。|确保客户端代码页和数据库排序规则代码页可以代表输入数据中的所有字符。 例如，若要插入波兰语字符，可以将客户端代码页设置为 1250（ANSI 中欧字符），并且数据库排序规则可以将波兰语用作排序规则指示符（例如，Polish_100_CI_AS_SC），或启用 UTF-8。|
|DBTYPE_STR|DBTYPE_WSTR|驱动程序从客户端代码页转换为 UTF-16 编码；服务器从 UTF-16 编码转换为列排序规则代码页。|确保客户端代码页可以代表输入数据中的所有字符。 例如，若要插入波兰语字符，可以将客户端代码页设置为 1250（ANSI 中欧字符）。|
|DBTYPE_WSTR|DBTYPE_STR|驱动程序从 UTF-16 编码转换为数据库排序规则代码页；服务器从数据库排序规则代码页转换为列排序规则代码页。|确保数据库排序规则代码页可以代表输入数据中的所有字符。 例如，若要插入波兰语字符，数据库排序规则代码页可以将波兰语用作排序规则指示符（例如，Polish_100_CI_AS_SC），或启用 UTF-8。|
|DBTYPE_WSTR|DBTYPE_WSTR|服务器从 UTF-16 转换为列排序规则代码页。|无。|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>从 UTF-8 编码的 CHAR 或 VARCHAR 列进行数据检索
为检索到的数据创建缓冲区时，使用 [DBBINDING 结构](https://go.microsoft.com/fwlink/?linkid=2071182)的数组描述缓冲区。 每个 DBBINDING 结构都会关联检索到的行中的单个列。 若要将列数据检索为 CHAR，请将 DBBINDING 结构的 wType  设置为 DBTYPE_STR。 若要将列数据检索为 WCHAR，请将 DBBINDING 结构的 wType  设置为 DBTYPE_WSTR。

对于结果缓冲区类型指示符 DBTYPE_STR，驱动程序将 UTF-8 编码的数据转换为客户端编码。 用户应确保客户端编码可以代表 UTF-8 列中的数据，否则可能会发生数据丢失。

对于结果缓冲区类型指示符 DBTYPE_WSTR，驱动程序将 UTF-8 编码的数据转换为 UTF-16 编码。

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>UTF-8 支持 (SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] 完全支持广泛使用的 UTF-8 字符编码作为导入或导出编码，或作为文本数据的数据库级或列级排序规则。 `CHAR` 和 `VARCHAR` 数据类型允许使用 UTF-8，并在创建或将对象的排序规则更改为带有 `UTF8` 后缀的排序规则时启用 UTF-8。

例如：将 `LATIN1_GENERAL_100_CI_AS_SC` 更改为 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 仅适用于支持增补字符的 Windows 排序规则，如 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中所引入的。 `NCHAR` 和 `NVARCHAR` 仅允许 UTF-16 编码，并保持不变。

此功能可能会节省大量存储空间，具体取决于正在使用的字符集。 例如，使用已启用 UTF-8 的排序规则将带 ASCII（拉丁）字符串的现有列数据类型从 `NCHAR(10)` 更改为 `CHAR(10)`，意味着将减少 50% 的存储需求。 存储需求减少是因为 `NCHAR(10)` 需要 20 个字节进行存储，而 `CHAR(10)` 需要 10 个字节存储相同的 Unicode 字符串。

有关详细信息，请参阅 [排序规则和 Unicode 支持](../../../relational-databases/collations/collation-and-unicode-support.md)。

**CTP 2.1** 现支持在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 安装期间默认选择 UTF-8 排序规则。

**CTP 2.2** 现支持将 UTF-8 字符编码与 SQL Server 复制结合使用。

**CTP 2.3** 现支持将 UTF-8 字符编码与 BIN2 排序规则 (UTF8_BIN2) 结合使用。

## <a name="see-also"></a>另请参阅  
[适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[适用于 SQL Server 的 OLE DB 驱动程序的 UTF-16 支持](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
