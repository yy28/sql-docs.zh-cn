---
title: 访问 Integration Services 服务 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6fdae3756442b1af660095fe53cbc8e4e3db82da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017145"
---
# <a name="access-to-the-integration-services-service"></a>访问 Integration Services 服务
  包保护级别可以限制允许谁来编辑和执行包。 需要其他保护来限制谁可以查看当前正在服务器上运行的包列表以及谁可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中停止当前正在执行的包。  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务来列出正在运行的包。 Windows Administrators 组的成员可以查看和停止所有当前正在运行的包。 如果用户不属于 Administrators 组的成员，则只能查看和停止他们启动的包。  
  
 请一定要限制对运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务（尤其是可以枚举远程文件夹的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务）的计算机的访问。 任何经过身份验证的用户都可以请求对包进行枚举。 即使该服务没有发现，也会枚举这些文件夹。 这些文件夹名称可能会对恶意用户非常有用。 如果管理员已经将该服务配置为枚举远程计算机上的文件夹，则用户也可能能够看到通常看不到的文件夹名称。  
  
  