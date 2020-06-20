---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3cc805042bff7259a311ca3f2acf4c26db59381b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031132"
---
# <a name="mssqlserver_50000"></a>MSSQLSERVER_50000
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|产品版本|11.0|  
|事件 ID|50000|  
|事件源|SETUP|  
|组件|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client{2}|  
|符号名称||  
|消息正文|尝试从文件“%.*ls”中读取内容时出现网络错误。|  
  
## <a name="explanation"></a>说明  
 尝试在满足以下条件的计算机上安装（或更新） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client：已安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，并且现有安装是来自从 sqlncli.msi 重命名的 MSI 文件。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的现有版本。 若要防止此错误，请不要从未命名为 sqlncli.msi 的 MSI 文件安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
## <a name="internal-only"></a>仅内部  
  
