---
title: "为 Sybase 组件 (SybaseToSQL) 删除 SSMA |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bd57909a4aade0a07da76f0e222fb21e58e643c3
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>为 Sybase 组件 (SybaseToSQL) 删除 SSMA
完成后将数据库迁移从 Sybase 自适应 Server Enterprise (ASE) 中，到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可能想要卸载 SSMA 组件。 你可以在任何时候，卸载客户端组件，但你不应卸载来自的扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]除非您确信你已迁移的数据库不再使用中的函数**ssma_syb**架构**sysdb**数据库。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>卸载 SSMA Sybase 客户端  
你可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载 SSMA**  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant 用于 Sybase**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
如果您确信你已迁移的数据库不使用中的对象**sysdb.ssma_syb**架构，则可以使用删除的扩展包**添加或删除程序**。  
  
若要卸载扩展包  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant Sybase 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在实用工具数据库脚本页的实例，单击**下一步**。  
  
5.  在连接参数页中，选择身份验证方法，，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到 SQL Server 的实例。 如果你选择 SQL Server 身份验证，你必须输入 SQL Server 登录名和密码。  
  
6.  在操作已完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
卸载后，你可以确认**sysdb.ssma_syb**架构，甚至整个**sysdb**数据库，是否使用已删除[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 但是，如果你使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果数据库存在并且可确保没有其他数据库引用此数据库中的对象，你可以分离数据库。  
  
## <a name="see-also"></a>另請參閱  
[安装适用于 Sybase 客户端 &#40; SSMASybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[在 SQL Server &#40; 上安装 SSMA 组件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  

