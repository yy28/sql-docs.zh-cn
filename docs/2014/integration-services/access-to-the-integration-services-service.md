---
title: 访问 Integration Services 服务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e9baff13c2bc368557a49b4509c6e48a444d583
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132117"
---
# <a name="access-to-the-integration-services-service"></a>访问 Integration Services 服务
  包保护级别可以限制允许谁来编辑和执行包。 需要其他保护来限制谁可以查看当前正在服务器上运行的包列表以及谁可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中停止当前正在执行的包。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务来列出正在运行的包。 Windows Administrators 组的成员可以查看和停止所有当前正在运行的包。 如果用户不属于 Administrators 组的成员，则只能查看和停止他们启动的包。  
  
 请一定要限制对运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务（尤其是可以枚举远程文件夹的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务）的计算机的访问。 任何经过身份验证的用户都可以请求对包进行枚举。 即使该服务没有发现，也会枚举这些文件夹。 这些文件夹名称可能会对恶意用户非常有用。 如果管理员已经将该服务配置为枚举远程计算机上的文件夹，则用户也可能能够看到通常看不到的文件夹名称。  
  
  
