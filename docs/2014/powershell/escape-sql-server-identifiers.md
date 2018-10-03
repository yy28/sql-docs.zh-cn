---
title: 对 SQL Server 标识符进行转义 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1df587280d7dbf42e22c7f472a792e6f401c79fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073787"
---
# <a name="escape-sql-server-identifiers"></a>对 SQL Server 标识符进行转义
  通常，可以使用 Windows PowerShell 反引号转义符 (`) 来对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 分隔标识符中允许使用但是 Windows PowerShell 路径名称中不允许使用的字符进行转义。 但是，对于某些字符，不能对其进行转义。 例如，不能对 Windows PowerShell 中的冒号字符 (:) 进行转义。 必须对包含该字符的标识符进行编码。 由于编码适用于所有字符，因此编码比转义可靠。  
  
## <a name="before-you-begin"></a>开始之前  
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
  
## <a name="see-also"></a>请参阅  
 [PowerShell 中的 SQL Server 标识符](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
