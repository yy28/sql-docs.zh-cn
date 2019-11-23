---
title: 在 SQL Server PowerShell 提供程序中指定实例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 9373de68-fd43-45f2-b9a6-149c96610aeb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 414d9135989c39ea183d14d2d6f5dfa6e84e6fe6
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797762"
---
# <a name="specify-instances-in-the-sql-server-powershell-provider"></a>在 SQL Server PowerShell 提供程序中指定实例
  为 SQL Server PowerShell 提供程序指定的路径必须标识它运行时所在的 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例和计算机。 用于指定计算机和实例的语法必须同时符合 SQL Server 标识符和 Windows PowerShell 路径的规则。  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To specify an instance:**  [Examples](#Examples)  
  
## <a name="before-you-begin"></a>开始之前  
 SQL Server 提供程序中的 SQLSERVER:\SQL 后的第一个节点是运行 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例的计算机的名称；例如：  
  
```  
SQLSERVER:\SQL\MyComputer  
```  
  
 如果在运行 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例的同一计算机上运行 Windows PowerShell，则可使用 localhost 或 (local)，而不使用计算机的名称。 使用 localhost 或 (local) 的脚本可在任何计算机上运行，而无需进行更改来反映不同计算机名称。  
  
 可以在同一台计算机上运行 [!INCLUDE[ssDE](../includes/ssde-md.md)] 可执行程序的多个实例。 SQL Server 提供程序路径中的计算机名称后的节点用于标识实例；例如：  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance  
```  
  
 每台计算机都有一个默认的 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例。 在安装默认实例时，无需为它指定名称。 如果在连接字符串中仅指定了计算机名称，则会连接到该计算机上的默认实例。 该计算机上的所有其他实例都必须是命名实例。 如果在安装过程中指定了实例名称，则必须在连接字符串中同时指定计算机名称和实例名称。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 您不能使用句点 (.) 在 PowerShell 脚本中指定本地计算机。 由于 PowerShell 会将句点解释为一个命令，因此不支持句点。  
  
 Windows PowerShell 通常会将 (local) 中的括号字符作为命令处理。 您必须对这些字符进行编码或转义才能在路径中使用它们，或用双引号将路径引起来。 有关详细信息，请参阅“SQL Server 标识符的编码和解码”。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序要求您始终指定实例名称。 对于默认实例，必须将实例名称指定为 DEFAULT。  
  
##  <a name="Examples"></a> 示例：计算机名称和实例名称  
 此示例使用 localhost 和 DEFAULT 来指定本地计算机上的默认实例：  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT
```  
  
 Windows PowerShell 通常会将 (local) 中的括号字符作为命令处理。 您必须：  
  
-   将路径字符串用引号引起来：  
  
    ```powershell
    Set-Location "SQLSERVER:\SQL\(local)\DEFAULT"  
    ```  
  
-   使用反引号字符 (`) 对括号进行转义：  
  
    ```powershell
    Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
    ```  
  
-   使用十六进制表示形式对括号进行编码：  
  
    ```powershell
    Set-Location SQLSERVER:\SQL\%28local%29\DEFAULT  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [PowerShell 中的 SQL Server 标识符](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供程序](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
