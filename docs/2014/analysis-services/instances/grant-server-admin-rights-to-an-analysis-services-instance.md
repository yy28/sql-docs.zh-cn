---
title: 授予服务器管理员权限（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 097b9a3fa27f2e2dfcfa506836055c940117aeb9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175256"
---
# <a name="grant-server-administrator-permissions-analysis-services"></a>授予服务器管理员权限 (Analysis Services)
  对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象和数据，该实例中的服务器管理员角色的成员具有无限访问权限。 用户必须是服务器管理员角色的成员才能执行任何服务器范围内的任务，如创建或处理数据库、修改服务器属性或启动跟踪（处理事件除外）。

 安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 时将建立角色成员身份。 在设置服务器时，运行安装程序的用户可以将他或他自己添加到该角色，或添加其他用户。 可以使用以下步骤将角色成员身份修改为安装后任务。

## <a name="modify-server-role-membership"></a>修改服务器角色成员身份

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，在对象资源管理器中右键单击实例名称，然后单击“属性”****。

2.  在 **“选择页”** 窗格中单击 **“安全性”** ，然后单击页底部的 **“添加”** 以将一个或多个 Windows 用户或组添加到服务器角色中。

     ![Management Studio 中的“添加用户”对话框](../media/ssas-serveradminadd.png "Management Studio 中的“添加用户”对话框")

 安装时，SQL Server 安装程序需要您指定至少一个用户帐户为 Analysis Services 系统管理员。

 默认情况下，还将为本地 Administrators 组的成员授予 Analysis Server 中的管理权限。 虽然未显式授予本地组 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务管理员角色中的成员身份，但是本地管理员可创建数据库、添加用户和权限以及执行系统管理员允许的任何其他任务。 此行为是可配置的。 它由`BuiltinAdminsAreServerAdmins`服务器属性确定，该属性默认设置为**true** 。 您可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中更改此属性。 有关详细信息，请参阅 [Security Properties](../server-properties/security-properties.md)。

 您还可以使用分析管理对象 (AMO) 来管理服务器角色。 有关详细信息，请参阅[使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。

## <a name="see-also"></a>另请参阅
 [授权 &#40;Analysis Services&#41;安全角色的对象和操作的访问权限](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md) [&#40;Analysis Services 多维数据&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)


