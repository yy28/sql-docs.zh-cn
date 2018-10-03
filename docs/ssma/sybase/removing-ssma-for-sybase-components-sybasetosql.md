---
title: 删除 SSMA for Sybase 组件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b3cebc9bb82778390716212fd3b5ae1bf800d3d3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47744805"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>删除 SSMA for Sybase 组件 (SybaseToSQL)
完成后将数据库从 Sybase Adaptive Server Enterprise (ASE) 中，为迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可能需要卸载 SSMA 组件。 您可以在任何时候，卸载客户端组件，但不是应卸载扩展包[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非你确信你迁移的数据库不能再使用中的函数**ssma_syb**架构**sysdb**数据库。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>卸载 SSMA for Sybase 客户端  
您可以通过使用卸载 SSMA**添加或删除程序**。  
  
**若要卸载的 SSMA**  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Sybase**，然后单击**删除**。  
  
3.  若要确认你想要卸载 SSMA，请单击**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸载扩展包  
如果您确信你迁移的数据库不使用中的对象**sysdb.ssma_syb**架构中，可以使用删除的扩展包**添加或删除程序**。  
  
若要卸载扩展包  
  
1.  在控制面板中，打开**添加或删除程序**。  
  
2.  选择**Microsoft SQL Server Migration Assistant for Sybase 扩展包**，然后单击**删除**。  
  
3.  若要确认你想要卸载扩展包，请单击**是**。  
  
4.  在与实用程序数据库脚本页的实例，单击**下一步**。  
  
5.  在连接参数页上，选择身份验证方法，然后依次**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到 SQL Server 实例。 如果您选择 SQL Server 身份验证，必须输入 SQL Server 登录名和密码。  
  
6.  在操作完成页上，单击**确定**。  
  
7.  在完成页上，单击**退出**。  
  
卸载后，你可以确认**sysdb.ssma_syb**架构，以及可能是整个**sysdb**数据库中，已删除通过使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 但是，如果使用其他 SSMA 产品，它们也使用**sysdb**数据库。 如果该数据库存在并且你将确保没有其他数据库引用此数据库中的对象，可以分离数据库。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Sybase 客户端&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server 上安装 SSMA 组件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
