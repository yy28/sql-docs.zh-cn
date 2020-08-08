---
title: 删除 SSMA for MySQL 组件 (MySQLToSql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 27c1ab67a6d62bceb31bb036978f65b3494e4f19
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935226"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>删除 SSMA for MySQL 组件 (MySQLToSql)
将数据库从 MySQL 迁移到之后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，你可能想要卸载 SSMA 组件。 你可以随时卸载客户端组件。 但是，如果你从卸载扩展包 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则 SSMA 将不再支持使用服务器端数据迁移引擎 (SQL Server/SQL Azure) 将数据从 MySQL 迁移到目标数据库。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>正在卸载 SSMA for MySQL 客户端  
可以使用 "**添加或删除程序**" 卸载 SSMA。  
  
**卸载 SSMA**  
  
1.  在“控制面板”中，打开“添加或删除程序”  。  
  
2.  选择 " **Microsoft SQL Server 迁移助手**"，然后单击 "**删除**"。  
  
3.  若要确认是否要卸载 SSMA，请单击 **"是"**。  
  
## <a name="uninstalling-the-extension-pack"></a>正在卸载扩展包  
可以使用 "**添加或删除程序**" 删除扩展包。  
  
**卸载扩展包**  
  
1.  在“控制面板”中，打开“添加或删除程序”  。  
  
2.  选择 " **Microsoft SQL Server 迁移助手**"，然后单击 "**删除**"。  
  
3.  若要确认是否要卸载扩展包，请单击 **"是"**。  
  
4.  在 "使用实用程序数据库脚本的实例" 页上，选择一个实例，然后单击 "**下一步**"。  
  
5.  在 "连接参数" 页上，选择身份验证方法，然后单击 "**下一步**"。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "身份验证"，则必须输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。  
  
6.  在 "操作已完成" 页上，单击 **"确定"**。  
  
7.  在 "完成" 页上，单击 "**退出**"。  
  
卸载过程完成后，您可以使用删除**ssma_MySQL sysdb**架构（可能为整个**sysdb**数据库）中的对象 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 但是，如果您使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果数据库存在并且您确信没有其他数据库引用此数据库中的对象，则可以分离该数据库。  
  
## <a name="see-also"></a>另请参阅  
[安装 SSMA for MySQL Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[在 SQL Server 上安装 SSMA 组件](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
