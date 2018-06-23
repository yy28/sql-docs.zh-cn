---
title: 配置数据库引擎访问的文件系统权限 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 02a84ea92555c74c0fed76b4f90b2d9c2337f46f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138486"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>配置数据库引擎访问的文件系统权限
  本主题说明如何授予 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]对存储数据库文件的位置的文件系统访问权限。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务必须具有 Windows 文件系统的权限才能访问存储数据库文件的文件夹。 在安装过程中配置对默认位置的权限。 如果您将数据库文件放在其他位置，可能需要按照这些步骤授予 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 对该位置的完全控制权限。  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，将权限分配给每个服务的服务 SID。 此系统可帮助提供更好的服务隔离和安全保护。 每个服务 SID 从服务名称派生得到，对每个服务是唯一的。 [配置 Windows 服务帐户和权限](configure-windows-service-accounts-and-permissions.md) 主题介绍了每个服务 SID，并提供 **Windows 特权和权限**一节中所述的名称。 必须为每个服务 SID 分配对文件位置的访问权限。  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>将文件系统权限授予每个服务 SID  
  
1.  使用 Windows 资源管理器，导航到存储数据库文件的文件系统位置。 右键单击文件系统文件夹，然后单击“属性”。  
  
2.  在 **“安全性”** 选项卡上，单击 **“编辑”**，然后单击 **“添加”**。  
  
3.  在 **“选择用户、计算机、服务帐户或组”** 对话框中，单击 **“位置”**，在位置列表的顶部选择您的计算机名称，然后单击 **“确定”**。  
  
4.  在**输入要选择的对象名称**框中，键入联机丛书主题中列出的每个服务 SID 名称**配置 Windows 服务帐户和权限**。 (有关[!INCLUDE[ssDE](../../includes/ssde-md.md)]每个服务 SID，使用**NT SERVICE\MSSQLSERVER**对于默认实例，或**NT SERVICE\MSSQL$ InstanceName**对于命名实例。)  
  
5.  单击 **“检查名称”** 以验证该条目。 验证经常失败，而且可能告知您找不到该名称。 单击 **“确定”** 时，将显示 **“找到多个名称”** 对话框。  
  
6.  现在选择每个服务 SID，则**MSSQLSERVER**或**NT SERVICE\MSSQL$ InstanceName**，然后单击**确定**。  
  
7.  再次单击 **“确定”** 以返回 **“权限”** 对话框。  
  
8.  在**组或用户**名称框中，选择每个服务 SID，然后在**权限**\<名称 > 中，选择**允许**的复选框**完全控制**。  
  
9. 单击 **“应用”**，然后单击 **“确定”** 两次以退出。  
  
## <a name="see-also"></a>请参阅  
 [管理数据库引擎服务](manage-the-database-engine-services.md)   
 [移动系统数据库](../../relational-databases/databases/system-databases.md)   
 [移动用户数据库](../../relational-databases/databases/move-user-databases.md)  
  
  