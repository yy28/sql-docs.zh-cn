---
title: 使用自定义字典自定义断字符的行为 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1fd6c83e02b15fcf126e5b3d078237c07d758cf3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032445"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>使用自定义词典自定义断字符的行为
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以通过创建特定于语言的自定义字典文件，为特定的语言自定义断字符的行为。 例如，您可以禁止断字符断开某些字词或模式。  
  
 有关详细信息，请参阅下列 SharePoint 文章：  
  
 [创建自定义字典 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请将自定义字典文件放置于以下文件夹中：  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 在创建或更改自定义字典文件后，使用以下命令重新启动 SQL 全文筛选器后台程序启动器：  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
