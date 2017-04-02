---
title: "对 SQL Server 标识符进行转义 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 对 SQL Server 标识符进行转义
  通常，可以使用 Windows PowerShell 反引号转义符 (`) 来对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔标识符中允许使用但是 Windows PowerShell 路径名称中不允许使用的字符进行转义。 但是，对于某些字符，不能对其进行转义。 例如，不能对 Windows PowerShell 中的冒号字符 (:) 进行转义。 必须对包含该字符的标识符进行编码。 由于编码适用于所有字符，因此编码比转义可靠。  
  
## 开始之前  
 反引号字符 (`) 键通常位于键盘左上角 ESC 键的下方。  
  
## 示例  
 下面是对 # 字符进行转义的示例：  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 下面是在（本地）指定为计算机名称时对括号进行转义的示例：  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## 另请参阅  
 [PowerShell 中的 SQL Server 标识符](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  