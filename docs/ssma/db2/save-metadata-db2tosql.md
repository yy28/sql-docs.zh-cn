---
title: 保存元数据 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a76083e-4902-449e-b125-7e9259fc37f7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d12ff5f349d5b7328af7e47dbfc7724420d6fb15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674975"
---
# <a name="save-metadata-db2tosql"></a>保存元数据 (DB2ToSQL)
**保存元数据**对话框会提示您保存它之前加载到 SSMA 项目的元数据。 这样，便有一个完整的项目文件，可以脱机使用，并发送给其他人，例如技术支持人员。  
  
访问**保存元数据**对话框中的，保存该项目。 如果缺少任何元数据，则将显示 SSMA**保存元数据**对话框。  
  
## <a name="options"></a>选项  
**名称**  
在项目中每个数据库的名称。  
  
**“状态”**  
指示如果元数据加载到 SSMA 项目，或缺少元数据。  
  
SSMA 到项目中根据需要加载元数据。 当您浏览元数据并将架构转换时，将自动加载元数据。  
  
**全选**  
选择所有列出的数据库。  
  
**Clear**  
清除该复选框对于丢失的元数据的所有数据库。 如果已加载元数据，不能清除复选框。  
  
**保存**  
保存项目，正在加载具有丢失的元数据的所选数据库的元数据。  
  
**取消**  
取消保存操作。 丢失的元数据不加载到项目。  
  
