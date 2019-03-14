---
title: 第 1 课：创建并应用 Off By Default 策略 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 88f5919c1bd36b912c2205da2032413ec39150f1
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579519"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>第 1 课：创建并应用 Off By Default 策略
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
通过使用基于策略的管理策略，您可以管理一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例、一个或多个实例对象、服务器实例、一个或多个数据库或者一个或多个数据库对象。 作为数据库管理员，您需要确保某些服务器没有启用数据库邮件。 在本课中，将创建一个条件以及设置此服务器选项的策略。 测试服务器以检查其是否符合该策略； 然后使用该策略重新配置服务器，以使服务器符合该策略。  

## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio，以及针对运行 SQL Server 的服务器的访问权限。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
  
## <a name="create-the-mail-off-condition"></a>创建 mail-Off 条件

1.  在对象资源管理器中，依次展开“管理”、“策略管理”和“方面”，右键单击“外围应用配置器”，然后单击“新建条件”。  

    ![新建条件](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  在“创建新条件”对话框的“名称”框中，输入 **Mail Off**。   
    1. 在“方面”框中，确认选择了“外围应用配置器”方面。
    1. 在“表达式”区域中，在“字段”框中选择 **@DatabaseMailEnabled**，在“运算符”框中选择 **=**，然后在“值”中选择“False”。  
    1. 在“说明”页上输入条件说明，然后单击“确定”以创建条件。  

    ![Mail off 条件](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>创建 off-by-default 策略  
  
1.  在对象资源管理器中，右键单击“外围应用配置器”，然后单击“新建策略”。  
  
2.  在“创建新策略”对话框的“名称”框中，输入 **Off By Default**。 
    1. 取消选中“已启用”复选框。 “已启用”复选框适用于自动策略，而此策略是按需执行的。
    1. 在“检查条件”复选框中，向下滚动到“外围应用配置器”区域，然后选择“Mail Off”作为要检查的条件。
    1. “针对目标”框为空，因为这是一个服务器范围内的策略。 
    1. 在“评估模式”复选框中，选择“按需”作为评估模式。
    1. 在“服务器限制”复选框中，选择“无”。
    1. 在“说明”页上，输入策略的说明。  

    ![off by default 策略](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. 在说明页，可以在“更多帮助超链接”区域中提供策略网页的超链接。 请在“要显示的文本”框中，输入为超链接显示的文本。
    1. 在“地址”框中输入“帮助”页的超链接，例如，公司 IT 部门的主页。
    1. 若要通过打开网页来确认地址是否正确，请单击“测试链接”。
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Off-by-default 策略 Web 链接](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>将服务器配置为运行 off-by-default 策略 

1.  在对象资源管理器中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，指向“策略”，然后单击“评估”。  

    ![评估策略](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  在“评估策略”对话框中，可以从另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或文件中选择策略。 对于此步骤，仍将“源”设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。  
    1. 在“策略”部分中，选择 **Off By Default** 策略。
    1. 要查看服务器是否符合该策略，请单击“评估”。
    1. 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 符合该策略，则会在“结果”区域中显示带复选标记的绿色圆圈。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不符合该策略，则会显示带 X 的红色圆圈。 

   ![评估 off-by-default 策略](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  在“目标详细信息”区域中，如果发生了错误，你会在“消息”列中看到其他信息。 在“消息”列中，单击“查看”以查看报表，其中包含所检查的每个方面属性的检查结果。 

    ![查看策略评估结果](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  页面底部将显示策略说明，“更多帮助”部分显示为策略配置的超链接。 单击消息超链接可打开在创建策略时指定的网页。   

1.  关闭浏览器，然后关闭“结果详细视图”对话框。  

1. 如果服务器不符合该策略并且你希望禁用数据库邮件，请在“评估结果”页中单击“应用”。  
  
10. 关闭“结果详细视图”和“评估策略”对话框。   

   
## <a name="next-lesson"></a>下一课  
[第 2 课：创建并应用命名标准策略](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
