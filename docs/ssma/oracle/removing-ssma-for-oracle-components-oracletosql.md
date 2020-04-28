---
title: 删除 Oracle 组件的 SSMA （OracleToSQL） |Microsoft Docs
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
manager: shamikg
ms.openlocfilehash: 0434f88c46d14672c84f5f7939488a827b229e27
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266565"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>删除 SSMA for Oracle 组件 (OracleToSQL)
将数据库从 Oracle 迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之后，你可能想要卸载 SSMA 组件。 你可以随时卸载客户端组件。 但是，除非您迁移的数据库不再使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysdb**数据库的**ssma_oracle**架构中的函数，否则不应从卸载扩展包。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>卸载 Oracle 客户端的 SSMA  
可以使用 "**添加或删除程序**" 卸载 SSMA。  
  
**卸载 SSMA**  
  
1.  在“控制面板”中，打开“添加或删除程序”  。  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)]选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "迁移助手**"，然后单击 "**删除**"。  
  
3.  若要确认是否要卸载 SSMA，请单击 **"是"**。  
  
## <a name="uninstalling-the-extension-pack"></a>正在卸载扩展包  
如果确定迁移的数据库不使用**ssma_oracle sysdb**架构中的对象，则可以使用 "**添加或删除程序**" 删除扩展包。  
  
**卸载扩展包**  
  
1.  在“控制面板”中，打开“添加或删除程序”  。  
  
2.  选择 " **Microsoft SQL Server 迁移助手" 作为 "Oracle 扩展包**"，然后单击 "**删除**"。  
  
3.  若要确认是否要卸载扩展包，请单击 **"是"**。  
  
4.  在 "使用实用程序数据库脚本的实例" 页上，选择一个实例，然后单击 "**下一步**"。  
  
5.  在 "连接参数" 页上，选择身份验证方法，然后单击 "**下一步**"。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "身份验证"，则必须[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]输入登录名和密码。  
  
6.  在 "操作已完成" 页上，单击 **"确定"**。  
  
7.  在 "完成" 页上，单击 "**退出**"。  
  
卸载后，你可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]删除 sysdb 架构中的对象（可能是整个**sysdb**数据库）来进行确认**ssma_oracle。** 但是，如果您使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果数据库存在并且您确定没有其他数据库引用此数据库中的对象，则可以分离该数据库。  
  
## <a name="see-also"></a>另请参阅  
[安装 SSMA for Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[在 SQL Server 上安装 SSMA 组件 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
