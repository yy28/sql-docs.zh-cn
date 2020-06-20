---
title: 在此版本的 SQL Server 中将不再支持 SQL Server 本机 SOAP。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80fd692b-1cea-4139-8e80-454d3e81c76d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7b1dd7c7ff564fc069e3a1ddecf1ff1ec9355d4f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036086"
---
# <a name="sql-server-native-soap-support-is-discontinued-in-this-version-of-sql-server"></a>在此版本的 SQL Server 中将不再支持 SQL Server 本机 SOAP。
  升级顾问检测到正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机 XML Web 服务。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中已移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机 XML Web 服务。  
  
## <a name="discovering-where-you-use-native-xml-web-services"></a>查找使用本机 XML Web 服务的场合  
 您可以看到您的应用程序使用本机 XML Web 服务的场合，如下所示：  
  
-   运行升级顾问时。  
  
-   升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本时。  
  
## <a name="corrective-action"></a>纠正措施  
 修改当前使用本机 XML Web 服务的应用程序。  
  
  
