---
title: "使用 sqlcmd 运行 Transact-SQL 脚本文件 | Microsoft Docs"
ms.custom: 
ms.date: 07/15/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8986c5788ed0223ada33369c9b30bec899596140
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="sqlcmd---run-transact-sql-script-files"></a>sqlcmd - 运行 Transact-SQL 脚本文件
 使用 **sqlcmd** 来运行 Transact-SQL 脚本文件。 Transact-SQL 脚本文件是一个文本文件，它可以包含 Transact-SQL 语句、 **sqlcmd** 命令以及脚本变量的组合。  

## <a name="create-a-script-file"></a>创建脚本文件  
 若要使用记事本创建一个简单的 Transact-SQL 脚本文件，请执行下列操作：  
  
1.  单击 **“开始”**，依次指向 **“所有程序”**、 **“附件”**，再单击 **“记事本”**。  
  
2.  复制以下 Transact-SQL 代码并将其粘贴到记事本：  
  
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
  
## <a name="run-the-script-file"></a>运行脚本文件  
  
1.  打开命令提示符窗口。  
  
2.  在命令提示符窗口中，键入： **sqlcmd -S myServer\instanceName -i C:\myScript.sql**  
  
3.  按 Enter。  
  
 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 员工的姓名和地址列表便会输出到命令提示符窗口。  

## <a name="save-the-output-to-a-text-file"></a>将输出保存到文本文件中
  
1.  打开命令提示符窗口。  
  
2.  在命令提示符窗口中，键入： **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**  
  
3.  按 Enter。  
  
 命令提示符窗口中不会返回任何输出， 而是将输出发送到 EmpAdds.txt 文件。 您可以打开 EmpAdds.txt 文件来查看此输出操作。  
  
## <a name="see-also"></a>另请参阅  
 [启动 sqlcmd 实用工具](../../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)  
  
  

