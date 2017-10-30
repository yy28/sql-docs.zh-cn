---
title: "为 MySQL 组件 (MySQLToSql) 删除 SSMA |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 765696847ddb1abd44dfac3463fdfd75f9a5c97a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>为 MySQL 组件 (MySQLToSql) 删除 SSMA
完成后将数据库迁移到 MySQL 从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可能想要卸载 SSMA 组件。 你可以随时卸载客户端组件。 但是，如果你卸载来自的扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然后，SSMA 将不再支持迁移到目标数据库 (SQL Server/SQL Azure) 使用服务器端数据迁移引擎从 MySQL 的数据。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>卸载 SSMA MySQL 客户端  
你可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载 SSMA**  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for MySQL**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
你可以使用删除的扩展包**添加或删除程序**。  
  
**若要卸载扩展包**  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant MySQL 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在实例上的实用工具数据库脚本一页，选择一个实例，然后单击**下一步**。  
  
5.  在连接参数页中，选择身份验证方法，，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果你选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，你必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码。  
  
6.  在操作已完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
卸载过程完成后，您可以确认在对象**sysdb.ssma_MySQL**架构，甚至整个**sysdb**数据库，是否使用已删除[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 但是，如果你使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果数据库存在并且可确保没有其他数据库引用到此数据库中的对象，你可以分离数据库。  
  
## <a name="see-also"></a>另請參閱  
[安装适用于 MySQL 客户端 &#40; SSMAMySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[在 SQL Server 上安装 SSMA 组件](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  

