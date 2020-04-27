---
title: SQL Server 代理属性（“警报系统”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00e3643a1beb3f69f8b370715001317e536c42e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245744"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>SQL Server 代理属性（“警报系统”页）
  使用此页可以查看和修改由[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理警报发送的消息的设置。  
  
## <a name="options"></a>选项  
 **邮件会话**  
 此部分中的选项用于配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理邮件。  
  
 **启用邮件配置文件**  
 启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理邮件。 默认情况下，不启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理邮件。  
  
 **邮件系统**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理要使用的邮件系统。 数据库邮件  
  
> [!NOTE]  
>  更改电子邮件系统后，必须重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务才能使更改生效。  
  
 **邮件配置文件**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理要使用的配置文件。 你还可以选择** \<"新建数据库邮件配置文件 ..." >** 创建新的配置文件。  
  
 **寻呼电子邮件**  
 使用此部分中的选项，可以配置发送给寻呼地址的电子邮件，以便与您的寻呼系统协同工作。  
  
 **寻呼电子邮件的地址格式**  
 使用此部分选项，可以指定包含在寻呼电子邮件中的地址和主题行的格式。  
  
 **“收件人”行**  
 指定邮件的“收件人”**** 行的选项  
  
 **前缀**  
 对于要发送给寻呼程序的邮件，键入系统要求在“收件人”**** 行开头显示的任何固定文本。  
  
 **寻呼程序**  
 在前缀和后缀之间包括邮件的电子邮件地址。  
  
 **后缀**  
 对于要发送给寻呼程序的邮件，键入寻呼系统要求在“收件人”**** 行末尾显示的任何固定文本。  
  
 **“抄送”行**  
 指定邮件的“抄送”**** 行的选项。  
  
 **前缀**  
 对于要发送给寻呼程序的邮件，键入系统要求在“抄送”**** 行开头显示的任何固定文本。  
  
 **寻呼程序**  
 在前缀和后缀之间包括邮件的电子邮件地址。  
  
 **后缀**  
 对于要发送给寻呼程序的邮件，键入寻呼系统要求在“抄送”**** 行末尾显示的任何固定文本。  
  
 **主题**  
 指定邮件主题的选项。  
  
 **前缀**  
 对于要发送给寻呼程序的邮件，键入寻呼系统要求在“主题”**** 行开头显示的任何固定文本。  
  
 **后缀**  
 对于要发送给寻呼程序的邮件，键入寻呼系统要求在“主题”**** 行末尾显示的任何固定文本。  
  
 **在通知消息中包含电子邮件正文**  
 在要发送给寻呼程序的消息中包含电子邮件的正文。  
  
 **防故障操作员**  
 使用此部分选项，可以指定防故障操作员的选项。  
  
 **启用防故障操作员**  
 指定防故障操作员。  
  
 **操作员**  
 设置要接收防故障通知的操作员的名称。  
  
 **通知方式**  
 设置用于通知防故障操作员的方式。  
  
 **标记替换**  
 使用此选项，可以启用作业步骤标记，这些标记能够用于由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报运行的作业。 有关作业步骤标记的详细信息，请参阅 [在作业步骤中使用标记](use-tokens-in-job-steps.md)。  
  
> [!IMPORTANT]  
>  任何对 Windows 事件日志具有写权限的 Windows 用户都可以访问由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报激活的作业步骤。 为了防范此安全隐患，默认情况下，可以在由警报激活的作业中使用的特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理标记已被禁用。 这些标记包括： **$(A-DBN)**、 **$(A-SVR)**、 **$(A-ERR)**、 **$(A-SEV)** 和 **$(A-MSG)**。  
>   
>  如果需要使用这些标记，请在启用它们之前，确保只有可信 Windows 安全组（例如 Administrators 组）的成员具有对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在计算机的事件日志的写权限。  
  
 **为警报的所有作业响应替换标记**  
 选中此复选框可以为由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 警报激活的作业启用标记替换。  
  
## <a name="see-also"></a>另请参阅  
 [运算符](operators.md)   
 [将 SQL Server 代理 Mail 配置为使用数据库邮件](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)   
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)  
  
  
