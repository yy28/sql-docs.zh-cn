---
title: 使用自定义字典自定义断字符的行为 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb02a47da20134925d9b2486ea0c08091af4aa6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055512"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>使用自定义词典自定义断字符的行为
  您可以通过创建特定于语言的自定义字典文件，为特定的语言自定义断字符的行为。 例如，您可以禁止断字符断开某些字词或模式。  
  
 有关详细信息，请参阅下列 SharePoint 文章：  
  
 [创建自定义字典 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请将自定义字典文件放置于以下文件夹中：  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 在创建或更改自定义字典文件后，使用以下命令重新启动 SQL 全文筛选器后台程序启动器：  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
