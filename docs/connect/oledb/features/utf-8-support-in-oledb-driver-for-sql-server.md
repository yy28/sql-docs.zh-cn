---
title: 适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: f410ddf4e3843936da6f93f488f379feea863e59
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744797"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序中的 UTF-8 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB 驱动程序的 SQL Server （版本 18.2.1） 添加了对 UTF-8 server 编码支持。 有关 SQL Server utf-8 支持的信息，请参阅：
- [排序规则和 Unicode 支持](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 支持 (CTP 2.2)](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-22)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>数据插入到 utf-8 编码的 CHAR 或 VARCHAR 列
在创建时插入的输入的参数缓冲区，使用一个数组描述缓冲区[DBBINDING 结构](https://go.microsoft.com/fwlink/?linkid=2071182)。 每个 DBBINDING 结构将使用者的缓冲区的单个参数相关联，并包含信息，例如长度和数据值的类型。 对于输入的参数的类型为 CHAR，缓冲区*wType*的 DBBINDING 结构应设置为 DBTYPE_STR。 对于输入的参数缓冲区的类型 WCHAR *wType*的 DBBINDING 结构应设置为 DBTYPE_WSTR。

当执行带有参数的命令，该驱动程序构造参数数据类型信息。 如果输入的缓冲区类型和参数数据类型匹配，驱动程序中不进行任何转换。 否则，该驱动程序将转换为参数数据类型的输入的参数缓冲区。 参数数据类型可显式设置由用户通过调用[icommandwithparameters:: Setparameterinfo](https://go.microsoft.com/fwlink/?linkid=2071577)。 如果未提供的信息，该驱动程序 （a） 列的元数据从服务器中检索时准备的语句，或 （b） 尝试从输入的参数数据类型的默认转换派生参数数据类型信息。

输入的参数缓冲区可能会转换为服务器列排序规则，该驱动程序或服务器，具体取决于输入的缓冲区的数据类型和参数数据类型。 在转换期间可能发生数据丢失，如果客户端代码页或数据库排序规则代码页不能表示在输入缓冲区中的所有字符。 下表介绍转换过程时将数据插入到 utf-8 启用列：

|缓冲区的数据类型|参数数据类型|转换|用户预防措施|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|服务器从客户端代码页转换到数据库的排序规则代码页;服务器转换为数据库排序规则代码页为列排序规则代码页。|确保客户端代码页和数据库排序规则代码页可以表示的输入数据中的所有字符。 例如，若要插入波兰语字符，客户端代码页无法设置为 1250 （ANSI 中欧语），且数据库排序规则可以作为排序规则指示符 (例如，Polish_100_CI_AS_SC) 使用波兰语，或者是 utf-8 启用。|
|DBTYPE_STR|DBTYPE_WSTR|驱动程序从客户端代码页转换到 utf-16 编码;服务器从 UTF 16 编码为列排序规则代码页转换。|请确保客户端代码页可以表示的输入数据中的所有字符。 例如，若要插入波兰语字符，客户端代码页可以设置为 1250 （ANSI 中欧语）。|
|DBTYPE_WSTR|DBTYPE_STR|从 utf-16 编码为数据库排序规则代码页; 驱动程序转换服务器转换为数据库排序规则代码页为列排序规则代码页。|请确保数据库排序规则代码页可以表示的输入数据中的所有字符。 例如，若要插入波兰语字符，数据库排序规则代码页无法波兰语用作排序规则指示符 (例如，Polish_100_CI_AS_SC) 或采用 utf-8 启用。|
|DBTYPE_WSTR|DBTYPE_WSTR|服务器转换为 utf-16 为列排序规则代码页。|无。|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>数据检索从 utf-8 编码的 CHAR 或 VARCHAR 列
在创建时检索到的数据的缓冲区，使用一个数组描述缓冲区[DBBINDING 结构](https://go.microsoft.com/fwlink/?linkid=2071182)。 每个 DBBINDING 结构将检索到的行中的单个列相关联。 若要检索为 CHAR 的列数据，请设置*wType*到 DBTYPE_STR 的 DBBINDING 结构。 若要检索的列数据作为 WCHAR，设置*wType*为 DBTYPE_WSTR 的 DBBINDING 结构。

结果缓冲区类型指示符 DBTYPE_STR，驱动程序将 utf-8 编码数据转换为编码的客户端。 用户应确保客户端编码来表示这些数据从 utf-8 列，否则为可能会发生数据丢失。

结果缓冲区类型指示符 DBTYPE_WSTR，驱动程序将 utf-8 编码数据转换为 utf-16 编码。
  
## <a name="see-also"></a>另请参阅  
[适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[适用于 SQL Server 的 OLE DB 驱动程序的 UTF-16 支持](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
