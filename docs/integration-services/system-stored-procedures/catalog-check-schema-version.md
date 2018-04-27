---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d0568db561467e05b73993fe183d0da179fb8d0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  确定 SSISDB 目录架构与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 二进制文件（ISServerExec 和 SQLCLR 程序集）是否兼容。  
  
 如果该架构与这些二进制文件不兼容，则 ISServerExec.exc 将记录错误消息。  
  
 当 SSISDB 架构在应用程序修补和升级过程中发生更改时，该架构版本将递增。 建议您在还原 SSISDB 备份之后运行下面的存储过程，以确保架构和二进制文件兼容。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>参数  
 [ @use32bitruntime= ] *use32bitruntime*  
 当此参数设置为 **True** 时，将调用 32 位版本的 dtexec。 *use32bitruntime* 为 **Bool**。  
  
## <a name="result-set"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>权限  
 此存储过程需要以下权限：  
  
-   **ssis_admin** 数据库角色的成员资格。  
  
  
