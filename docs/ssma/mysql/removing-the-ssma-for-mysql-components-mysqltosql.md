---
title: 删除 SSMA for MySQL 组件 (MySQLToSql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: adab686126cb608ae32870a9a138720b77d212bf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394222"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>删除 SSMA for MySQL 组件 (MySQLToSql)
当您已完成从 mysql 迁移到将数据库迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能需要卸载 SSMA 组件。 您可以在任何时候卸载客户端组件。 但是，如果卸载扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后，SSMA 将不再支持的数据从 MySQL 复制到目标数据库 (SQL Server/SQL Azure) 使用服务器端数据迁移引擎迁移。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>卸载 SSMA for MySQL 客户端  
您可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载的 SSMA**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for MySQL**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，请单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
可以使用删除的扩展包**添加或删除程序**。  
  
**若要卸载扩展包**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for MySQL 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在与实用程序数据库脚本页的实例，选择一个实例，然后单击**下一步**。  
  
5.  在连接参数页上，选择身份验证方法，然后依次**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码。  
  
6.  在操作完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
卸载过程完成后，你可以确认的对象中**sysdb.ssma_MySQL**架构，以及可能是整个**sysdb**数据库中，已删除通过使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 但是，如果使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果该数据库存在并且你将确保此数据库中的对象引用的其他数据库，可以分离数据库。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for MySQL 客户端&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[在 SQL Server 上安装 SSMA 组件](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
