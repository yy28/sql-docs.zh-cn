---
title: " (AccessToSQL) 保存元数据 |Microsoft Docs"
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fa4ce8ad-9935-4195-90f9-3fdac587a4ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7f0f9b22d571e4ac89fcd0db464a1e79ae91a28b
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933911"
---
# <a name="save-metadata-accesstosql"></a> (AccessToSQL) 保存元数据
保存**元数据**对话框会提示您在保存之前将元数据加载到 SSMA 项目中。 这样，你就可以拥有一个完整的项目文件，你可以脱机使用该文件并将其发送给其他人，例如技术支持人员。  
  
若要访问 "**保存元数据**" 对话框，请保存该项目。 如果缺少任何元数据，SSMA 将显示 "**保存元数据**" 对话框。  
  
## <a name="options"></a>选项  
**名称**  
项目中每个数据库的名称。  
  
**状态**  
指示元数据是否已加载到 SSMA 项目中，或元数据是否缺失。  
  
SSMA 根据需要将元数据加载到项目中。 浏览元数据和转换架构时，会自动加载元数据。  
  
**全选**  
选择所有列出的数据库。  
  
**清除**  
清除缺少元数据的所有数据库的复选框。 如果已加载元数据，则不能清除此复选框。  
  
**保存**  
保存项目，为缺少元数据的所选数据库加载元数据。  
  
**取消**  
取消保存操作。 缺少元数据不会加载到项目中。  
  
