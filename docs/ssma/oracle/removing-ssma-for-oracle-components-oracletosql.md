---
title: 删除 SSMA for Oracle 组件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da54f9fc21b74be790ac86c9690738b71fd3e1c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628542"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>删除 SSMA for Oracle 组件 (OracleToSQL)
当您已完成从 oracle 迁移到将数据库迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能需要卸载 SSMA 组件。 您可以在任何时候卸载客户端组件。 但是，不应卸载扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非你已迁移的数据库不能再使用中的函数**ssma_oracle**的架构**sysdb**数据库。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>卸载 SSMA for Oracle 客户端  
您可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载的 SSMA**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，请单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
如果您确信你迁移的数据库不使用中的对象**sysdb.ssma_oracle**架构中，可以使用删除的扩展包**添加或删除程序**。  
  
**若要卸载扩展包**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Oracle 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在与实用程序数据库脚本页的实例，选择一个实例，然后单击**下一步**。  
  
5.  在连接参数页上，选择身份验证方法，然后依次**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码。  
  
6.  在操作完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
在卸载后，可以确认的对象中**sysdb.ssma_oracle**架构，以及可能是整个**sysdb**数据库中，已删除通过使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 但是，如果使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果该数据库存在并且你将确保没有其他数据库引用此数据库中的对象，可以分离数据库。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Oracle 客户端&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server 上安装 SSMA 组件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
