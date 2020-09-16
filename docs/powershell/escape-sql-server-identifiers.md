---
title: 对 SQL Server 标识符进行转义 | Microsoft Docs
description: Windows PowerShell 路径中不支持出现在 SQL Server 分隔标识符中的某些字符。 了解其中某些字符如何使用反引号字符进行转义。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c7896c2f0368826698b29aab5d1f8d52ae9ad22d
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714035"
---
# <a name="escape-sql-server-identifiers"></a>对 SQL Server 标识符进行转义
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

通常，可以使用反引号转义符 (`) 来对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分隔标识符中允许使用但是 Windows PowerShell 路径名称中不允许使用的字符进行转义。 但是，对于某些字符，不能对其进行转义。 例如，不能对 Windows PowerShell 中的冒号字符 (:) 进行转义。 必须对包含该字符的标识符进行编码。 由于编码适用于所有字符，因此编码比转义可靠。  

> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS 。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能 。
> 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。
> 要安装 SqlServer 模块，请参阅[安装 SQL Server PowerShell](download-sql-server-ps-module.md)。

反引号字符 (`) 键通常位于键盘左上角 ESC 键的下方。  
  
## <a name="examples"></a>示例  
 下面是对 # 字符进行转义的示例：  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 下面是在（本地）指定为计算机名称时对括号进行转义的示例：  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>另请参阅  
 [PowerShell 中的 SQL Server 标识符](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供程序](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
