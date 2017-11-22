---
title: "为 Oracle 组件 (OracleToSQL) 删除 SSMA |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: e0dea581d93f996f710a64bf35c8d208740b1d17
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>为 Oracle 组件 (OracleToSQL) 删除 SSMA
完成后将数据库迁移到的 Oracle 从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可能想要卸载 SSMA 组件。 你可以随时卸载客户端组件。 但是，你不应卸载来自的扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]除非你已迁移的数据库不再使用中的函数**ssma_oracle**架构**sysdb**数据库。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>用于 Oracle 客户端卸载 SSMA  
你可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载 SSMA**  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Oracle**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
如果您确信你已迁移的数据库不使用中的对象**sysdb.ssma_oracle**架构，则可以使用删除的扩展包**添加或删除程序**。  
  
**若要卸载扩展包**  
  
1.  在 Control Panel 中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Oracle 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在实例上的实用工具数据库脚本一页，选择一个实例，然后单击**下一步**。  
  
5.  在连接参数页中，选择身份验证方法，，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果你选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，你必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码。  
  
6.  在操作已完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
在卸载后你可以确认在对象**sysdb.ssma_oracle**架构，甚至整个**sysdb**数据库，是否使用已删除[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 但是，如果你使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果数据库存在并且可确保没有其他数据库引用此数据库中的对象，你可以分离数据库。  
  
## <a name="see-also"></a>另请参阅  
[安装适用于 Oracle 客户端 &#40; OracleToSQL &#41; SSMA](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[在 SQL Server &#40; OracleToSQL &#41; 上安装 SSMA 组件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
