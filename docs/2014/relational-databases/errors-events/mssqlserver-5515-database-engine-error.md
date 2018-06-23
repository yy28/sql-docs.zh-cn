---
title: MSSQLSERVER_5515 | Microsoft Docs
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
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c719c62ecc805be3c3102b0e3457596ab2561817
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018455"
---
# <a name="mssqlserver5515"></a>MSSQLSERVER_5515
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|5515|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|FS_OPEN_CONTAINER_FAILED|  
|消息正文|无法打开 FILESTREAM 文件的容器目录“%.*ls”。 操作系统返回 Windows 状态代码 0x%x。|  
  
## <a name="explanation"></a>解释  
 无法打开为 FILESTREAM 文件指定的容器目录。  
  
## <a name="user-action"></a>用户操作  
 请查看具体的 Windows 状态代码以了解错误原因。 有关详细信息，请参阅[事件和错误消息中心](http://go.microsoft.com/fwlink/?linkid=47660)。  
  
  