---
title: 对 SQL Server 标识符进行编码和解码 | Microsoft Docs
description: SQL Server 分隔标识符有时候包含 Windows PowerShell 路径中不支持的字符。 了解如何在 SQL Server 分隔标识符中用十六进制值来表示这些字符。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51e4caad8209f84a1ab0f1db054431c37cd10598
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714055"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>对 SQL Server 标识符进行编码和解码
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SQL Server 分隔标识符有时候包含 Windows PowerShell 路径中不支持的字符。 可以通过对其十六进制值进行编码来指定这些字符。  

> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS 。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能 。  
> 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。
> 要安装 SqlServer 模块，请参阅[安装 SQL Server PowerShell](download-sql-server-ps-module.md)。
  
  
对于 Windows PowerShell 路径名称中不支持的字符，可以表示或编码为“%”字符后跟代表该字符的位模式的十六进制值（如“ **%** xx”）。 对于 Windows PowerShell 路径中不支持的字符，始终可以使用编码来处理字符。  
  
 **Encode-SqlName** cmdlet 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 标识符作为输入。 它输出一个字符串，其中包含所有不受 Windows PowerShell 语言支持且已经用“%xx”编码的字符。 **Decode-SqlName** cmdlet 将经过编码的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 标识符作为输入并返回初始标识符。  
  
##  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 Encode-Sqlname 和 Decode-Sqlname cmdlet 仅对 SQL Server 分隔标识符中允许但在 PowerShell 路径中不受支持的字符进行编码和解码********。 下面是通过 Encode-SqlName 编码并可通过 Decode-SqlName 解码的字符 ：  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**字符**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**十六进制编码**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="encoding-an-identifier"></a><a name="EncodeIdent"></a> 对标识符进行编码  
 **对 PowerShell 路径中的 SQL Server 标识符进行编码**  
  
-   使用以下两种方法之一对 SQL Server 标识符进行编码：  
  
    -   使用语法 %XX（其中，XX 是十六进制代码）为不支持的字符指定十六进制代码。  
  
    -   将标识符以带引号的字符串形式传递到 **Encode-Sqlname** cmdlet  
  
### <a name="examples-encoding"></a>示例（编码）  
 此示例指定“:”字符 (%3A) 的编码版本：  
  
```  
Set-Location Table%3ATest  
```  
  
 或者，可以使用 **Encode-SqlName** 生成受 Windows PowerShell 支持的名称：  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="decoding-an-identifier"></a><a name="DecodeIdent"></a> 对标识符进行解码  
 **对 PowerShell 路径中的 SQL Server 标识符进行解码**  
  
 使用 **Decode-Sqlname** cmdlet 将十六进制编码替换为该编码所表示的字符。  
  
### <a name="examples-decoding"></a>示例（解码）  
 下面的示例返回“Table:Test”：  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>另请参阅  
 [PowerShell 中的 SQL Server 标识符](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供程序](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
