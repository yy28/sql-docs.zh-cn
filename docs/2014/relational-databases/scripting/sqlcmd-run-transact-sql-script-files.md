---
title: 使用 sqlcmd 运行 Transact-SQL 脚本文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ff18203f0120210f3443973ed7e44761b84ac8ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125081"
---
# <a name="run-transact-sql-script-files-using-sqlcmd"></a>使用 sqlcmd 运行 Transact-SQL 脚本文件
  您可以使用 `sqlcmd` 运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件。 A[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本文件是文本文件，可以包含的组合[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，`sqlcmd`命令和脚本变量。  
  
 若要使用记事本创建一个简单的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件，请执行下列操作：  
  
1.  单击 **“开始”**，依次指向 **“所有程序”**、 **“附件”**，再单击 **“记事本”**。  
  
2.  复制并粘贴以下[!INCLUDE[tsql](../../includes/tsql-md.md)]到记事本的代码：  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  在 C 驱动器中将文件保存为 **myScript.sql** 。  
  
### <a name="to-run-the-script-file"></a>运行脚本文件  
  
1.  打开命令提示符窗口。  
  
2.  在命令提示符窗口中，键入： `sqlcmd -S myServer\instanceName -i C:\myScript.sql`  
  
3.  按 Enter。  
  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 员工的姓名和地址列表便会输出到命令提示符窗口。  
  
### <a name="to-save-this-output-to-a-text-file"></a>将此输出保存到文本文件中  
  
1.  打开命令提示符窗口。  
  
2.  在命令提示符窗口中，键入： `sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt`  
  
3.  按 Enter。  
  
 命令提示符窗口中不会返回任何输出， 而是将输出发送到 EmpAdds.txt 文件。 您可以打开 EmpAdds.txt 文件来查看此输出操作。  
  
## <a name="see-also"></a>请参阅  
 [启动 sqlcmd 实用工具](sqlcmd-start-the-utility.md)   
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  