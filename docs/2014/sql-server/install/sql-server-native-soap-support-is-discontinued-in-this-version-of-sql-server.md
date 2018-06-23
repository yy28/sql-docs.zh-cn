---
title: 在此版本的 SQL Server 中将不再支持 SQL Server 本机 SOAP。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80fd692b-1cea-4139-8e80-454d3e81c76d
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 31dbc731e6c83ddc3d3587a95a158fb2e7362e3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137450"
---
# <a name="sql-server-native-soap-support-is-discontinued-in-this-version-of-sql-server"></a>在此版本的 SQL Server 中将不再支持 SQL Server 本机 SOAP。
  升级顾问检测到正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机 XML Web 服务。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中已移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机 XML Web 服务。  
  
## <a name="discovering-where-you-use-native-xml-web-services"></a>查找使用本机 XML Web 服务的场合  
 您可以看到您的应用程序使用本机 XML Web 服务的场合，如下所示：  
  
-   运行升级顾问时。  
  
-   升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本时。  
  
## <a name="corrective-action"></a>纠正措施  
 修改当前使用本机 XML Web 服务的应用程序。  
  
  