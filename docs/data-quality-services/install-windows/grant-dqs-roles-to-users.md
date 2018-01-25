---
title: "授予用户 DQS 角色 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: afb445b5-bdbe-4bfe-844f-344766cdc2b2
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87a0ded8ffda133711505c2da948d09909b8046a
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="grant-dqs-roles-to-users"></a>将 DQS 角色授予用户
  本主题介绍如何基于 Windows 主体创建 SQL 登录名，以及如何授予针对 DQS_MAIN 数据库的 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 角色。  
  
## <a name="prerequisites"></a>必备条件  
  
-   您必须已通过运行 DQSInstaller.exe 文件完成了 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安装。 有关详细信息，请参阅 [运行 DQSInstaller.exe 以便完成数据质量服务器安装](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)。  
  
-   若要创建 SQL 登录名以及授予他们 DQS 角色，您的 Windows 用户帐户必须是适当固定服务器角色的成员（例如 securityadmin、serveradmin 或 sysadmin）。  
  
### <a name="to-create-sql-login-and-grant-dqs-roles"></a>创建 SQL 登录名并授予 DQS 角色  
  
1.  启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开您的 SQL Server 实例，然后展开 **“安全性”**。  
  
3.  右键单击“安全性”文件夹，指向“新建”，然后单击“登录名”。  
  
4.  在 **“登录名 - 新建”** 对话框中，在 **“登录名”** 框中指定 Windows 用户的名称，将身份验证类型指定为 **“Windows 身份验证”**，然后单击 **“搜索”** 以验证此用户。  
  
5.  在验证该用户后，在左侧窗格中单击 **“用户映射”** 。  
  
6.  在右侧窗格中，选中 **DQS_MAIN** 数据库的“映射”列下的复选框，然后根据用户所需的访问级别，在“数据库角色成员身份: DQS_MAIN”窗格中选中 **dqs_administrator**、**dqs_kb_editor** 或 **dqs_kb_operator** 复选框。 有关这三个 DQS 角色的信息，请参阅 [DQS Security](../../data-quality-services/dqs-security.md)。  
  
7.  在 **“登录名 - 新建”** 对话框中，单击 **“确定”** 以便应用更改。  
  
    > [!NOTE]  
    >  如果你向某一用户授予 **dqs_administrator** 角色，应用更改，然后重新选中用户权限，则其他两个 DQS 角色复选框（**dq_kb_editor** 和 **dqs_kb_operator**）也将被选中。  
  
## <a name="next-steps"></a>Next Steps  
 尝试通过使用您刚刚为其创建了 SQL 登录名并授予了 DQS 角色的 Windows 用户帐户登录到 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [安装 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [创建登录名](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
