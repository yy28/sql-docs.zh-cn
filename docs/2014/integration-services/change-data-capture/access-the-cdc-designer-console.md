---
title: 访问 CDC 设计器控制台 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a452fd2b33d170aad484535d0bc0c7f71b065fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126588"
---
# <a name="access-the-cdc-designer-console"></a>访问 CDC 设计器控制台
  您可以从安装了 CDC 设计器控制台的计算机访问该控制台。 有关安装的详细信息，请参阅“安装”。  
  
 在您打开 CDC 设计器控制台时，“连接到 SQL Server”对话框将打开。  
  
 访问该 CDC 设计器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名必须对 MSXDBCDC 数据库具有 UPDATE 权限。 此外，该登录名还必须具有 `dbcreator` 固定服务器角色，以便创建新的 Oracle CDC 实例。 建议该登录名还具有对要使用的 CDC 数据库的 SELECT 权限，否则，该用户将无法查看这些数据库的状态。  
  
 在“连接到 SQL Server”对话框中输入以下信息。  
  
### <a name="server-name"></a>服务器名称  
 键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的服务器的名称。  
  
### <a name="authentication"></a>身份验证  
 选择下列选项之一：  
  
-   **Windows 身份验证**  
  
-   **SQL Server 身份验证**：如果选择此选项，则必须在连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中为用户键入“登录名”和“密码”。  
  
 该登录名必须具有允许访问 MSXCDCDB 数据库的数据库角色。 建议该登录名还具有访问要使用的任何其他数据库的权限，否则，该用户将无法查看这些数据库中的数据。  
  
### <a name="options"></a>“常规”  
 单击箭头可以查看要配置的可用选项。 您可以选择保留这些选项不变，使用其默认值。 可用选项是：  
  
 **连接超时值**  
 键入一个时间（秒钟），未超过该时间，Oracle CDC 服务将等待与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接，超过该时间后即超时。默认值为 **15**。  
  
 **执行超时值**  
 键入一个时间（秒钟），未超过该时间，Oracle CDC Windows 服务将等待命令执行，超过该时间后即超时。默认值为 **30**。  
  
 **加密连接**  
 选择“加密连接”将使用加密连接进行 Oracle CDC 服务和目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之间的通信。**高级**：单击“高级”并根据需要在“高级连接属性”对话框中键入任何附加的连接属性。  
  
 **高级**  
 单击“高级”并根据需要在“高级连接属性”对话框中键入任何附加的连接属性。  
  
 有关“高级连接属性”对话框的信息，请参阅[高级连接属性](advanced-connection-properties.md)。  
  
## <a name="see-also"></a>请参阅  
 [针对 CDC 设计器的 SQL Server 连接所需权限](sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  