---
title: "创建或编辑服务器组 (SQL Server Management Studio)| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.editgroup.f1
- sql13.swb.newgroup.f1
helpviewer_keywords:
- Registered Servers [SQL Server], server groups
- server groups [SQL Server]
- groups [SQL Server], server
ms.assetid: d4a942bd-2dd1-42db-ad0e-e9a9ae5b856d
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2bb7c1950d3a8dd84b6c5445bc48bf1ab104887
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="create-or-edit-a-server-group-sql-server-management-studio"></a>创建或编辑服务器组 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 本主题说明如何通过创建服务器组并将服务器放入服务器组中，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中整理已注册服务器中的服务器。 可以随时在已注册的服务器中创建服务器组，也可以在注册服务器时创建服务器组。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-server-group-in-registered-servers"></a>在已注册的服务器中创建服务器组  
  
1.  在已注册的服务器中，单击“已注册的服务器”工具栏上的服务器类型。 如果“已注册的服务器”不可见，请在 **“视图”** 菜单上，单击 **“已注册的服务器”** 。  
  
2.  右键单击某服务器或服务器组，指向“新建”，然后单击“服务器组”。  
  
3.  在 **“新建服务器组”** 对话框的 **“组名”** 列表框中，键入服务器组的唯一名称。 在“已注册的服务器”树中的当前位置，服务器组名必须唯一。  
  
4.  在 **“组说明”** 列表框中，选择性地键入一个描述服务器组的友好名称，例如，“Finance Servers for Latin America”。  
  
5.  在 **“选择新服务器组的位置”** 框中，单击一个用于存放该组的位置，再单击 **“保存”**。  
  
    > [!NOTE]  
    >  注册服务器时，还可以通过单击“新建组”并完成“新建组”对话框，创建新服务器组。  
  
## <a name="see-also"></a>另请参阅  
 [注册服务器](../../tools/sql-server-management-studio/register-servers.md)  
  
  
