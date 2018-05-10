---
title: 连接到 Oracle 源数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1c81c8db6c0f91493f9bef023c6e09b5c00f9648
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-an-oracle-source-database"></a>连接到 Oracle 源数据库
  使用“Oracle 源”页可提供连接到 Oracle 源数据库所需的信息。 CDC 实例将读取您连接到的 Oracle 数据库的重做日志。  
  
 **Oracle 连接字符串**  
 输入正使用 Oracle 数据库的计算机的 Oracle 连接字符串。 连接字符串按以下方法之一编写：  
  
 `host[:port][/service name]`  
  
 连接字符串还可以指定 Oracle Net 连接描述符，例如 `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 如果使用目录服务器或 tnsnames，则连接字符串可以是连接的名称。  
  
 **Oracle 日志挖掘身份验证**  
 若要输入授权执行日志挖掘的 Oracle 数据库用户的凭据，请选择下列选项之一：  
  
-   **Windows 身份验证**：选择此选项可使用当前的 Windows 域凭据。 只有当 Oracle 数据库配置为使用 Windows 身份验证时，才可以使用此选项。  
  
-   **Oracle 身份验证**：如果选择此选项，则必须在您连接到的 Oracle 数据库中为用户键入 **“用户名”** 和 **“密码”** 。  
  
> [!NOTE]  
>  用户必须在 Oracle 数据库中被授予以下权限才能成为日志挖掘用户。  
>   
>  -   SELECT on \<any-captured-table>  
> -   SELECT ANY TRANSACTION  
> -   EXECUTE on DBMS LOGMNR  
> -   SELECT on V$LOGMNR CONTENTS  
> -   SELECT on V$ARCHIVED LOG  
> -   SELECT on V$LOG  
> -   SELECT on V$LOGFILE  
> -   SELECT on V$DATABASE  
> -   SELECT on V$THREAD  
> -   SELECT on ALL INDEXES  
> -   SELECT on ALL OBJECTS  
> -   SELECT on DBA OBJECTS  
> -   SELECT on ALL TABLES  
>   
>  如果无法将上述任何权限授予 V$xxx，则向其授予 V_S$xxx。  
  
 **测试连接**  
 单击“测试连接”可确定是否已建立与具有 Oracle 数据库的远程计算机的连接。 将打开一个对话框，通知您连接是否成功。  
  
> [!IMPORTANT]  
>  由于一个已知问题，如果 CDC 设计器未以管理员的身份运行，与 Oracle 源数据库的连接可能会失败。 如果连接失败，请使用 **“以管理员身份运行”** 选项关闭后重新启动 CDC 设计器。  
  
 在此页上输入完信息后，单击 **“下一步”** 以便 [Select Oracle Tables and Columns](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何创建 SQL Server 更改数据库实例](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [编辑实例属性](../../integration-services/change-data-capture/edit-instance-properties.md)  
  
  
