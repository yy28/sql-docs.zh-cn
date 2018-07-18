---
title: MSSQLSERVER_3169 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc119c1ebfc2c587bf12fb8337194e7516e4781c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423366"
---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3169|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|不适用|  
|消息正文|该数据库是在运行版本 %ls 的服务器上备份的。 该版本与此服务器(运行版本 %ls)不兼容。 请在支持该备份的服务器上还原该数据库，或者使用与此服务器兼容的备份。|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的某些功能会影响数据库文件的结构。 将数据库还原到另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，文件格式可能会与不同版本的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]不兼容。  
  
 例如，如果在较高版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 vardecimal 存储格式，然后尝试在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 之前的版本中还原数据库文件，便可能导致此错误。  
  
## <a name="user-action"></a>用户操作  
 确定在发起服务器上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本。 在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，右键单击服务器，然后单击**属性**或类型`SELECT @@VERSION`在查询窗口中。 通过使用原始版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 打开数据库。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中调查已在原始数据库中启用的功能。 修改这些设置以使该设置能用于数据库要在其中进行还原的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
  
