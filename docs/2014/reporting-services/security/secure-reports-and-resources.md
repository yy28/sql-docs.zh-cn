---
title: 保护报表和资源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 20d800cc906a3953fe2f5143e980fd2e869ec318
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964413"
---
# <a name="secure-reports-and-resources"></a>保护报表和资源
  您可以设置各个报表和资源的安全性，以控制用户对这些项的访问权限。 默认情况下，只有是“管理员”内置组的成员的用户，才能运行报表、查看资源、修改属性以及删除项。 所有其他用户必须具有为其创建的角色分配才能访问报表或资源。  
  
## <a name="role-based-access-to-reports-and-resources"></a>对报表和资源的基于角色的访问  
 若要授予报表和资源的访问权限，则可以允许用户从父文件夹继承现有的角色分配，也可以针对项本身创建新的角色分配。  
  
 在大多数情况下，您可能需要使用从父文件夹继承的权限。 只有在需要隐藏报表或资源以防止不需要了解该报表或资源存在与否的用户看到它们，或需要提高报表或项的访问级别时，才有必要对各个报表和资源设置安全性。 这些目标并不相互冲突。 您可以限定只有一小部分用户能够访问报表，并向其中的部分用户或全部用户另外授予管理报表的权限。  
  
 您可能需要创建多个角色分配来实现目标。 例如，假设您希望两个用户 Ann 和 Fernando 以及人力资源经理组可以访问某个报表。 Ann 和 Fernando 需要能够管理该报表，而人力资源经理组的成员则只需运行该报表。 为了满足所有这些用户的需要，您可以分别创建三个角色分配，一个角色分配使 Ann 成为报表的内容管理员，另一个使 Fernando 成为报表的内容管理员，第三个则支持人力资源经理组对报表执行只读访问任务。  
  
 在您设置了报表或资源的安全性后，即使这些项移至新位置，也会一直保留这些设置。 例如，如果您移动了只有少数几个人可以访问的报表，那么，即使移动后的新位置是一个安全策略相对开放的文件夹，也只有原来的那几个人才能访问该报表。  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>减少已发布报表或文档中的 HTML 注入攻击  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，报表和资源是在运行报表的用户的安全标识下处理的。 如果报表中包含表达式、脚本、自定义报表项或自定义程序集，则代码将在用户的凭据下运行。 如果资源是包含脚本的 HTML 文档，则当用户在报表服务器中打开文档时，该脚本即会运行。 尽管运行报表中的脚本或代码的能力是一项强大的功能，但具有一定程度的风险。 如果是恶意代码，则报表服务器和运行报表的用户就很容易受到攻击。  
  
 授予对以 HTML 格式处理的报表和资源的访问权限时，要注意报表是在完全信任权限下处理的而且可能会将潜在的恶意脚本发送到客户端，这一点非常重要。 根据浏览器设置，客户端将在浏览器中指定的信任级别执行 HTML。  
  
 可以通过采取以下预防措施来降低运行恶意脚本的风险：  
  
-   决定谁可以将内容发布到报表服务器时，应慎重选择。 由于存在发布恶意内容的可能性，因此应将可发布内容的用户限制到少数受信任的用户。  
  
-   所有的发布者都应避免发布来自未知源或不可信源的报表和资源。 如果必要，请在文本编辑器中打开文件并查找可疑脚本和 URL。  
  
## <a name="report-parameters-and-script-injection"></a>报表参数和脚本注入  
 报表参数为报表的总体设计和执行提供灵活性。 但是，在某些情况下，引诱攻击中的攻击者也可以利用这种灵活性。 若要降低无意中运行恶意脚本的风险，请仅从可信来源打开呈现的报表。 建议您考虑以下这种潜在 HTML 呈现器脚本注入攻击的情况：  
  
1.  报表包含一个文本框，该框有一个超链接操作设置为可能包含恶意文本的参数值。  
  
2.  报表将发布到报表服务器，或可能通过这样一种方式提供：可从 Web 页的 URL 控制报表参数值。  
  
3.  攻击者创建一个链接，该链接指向用于指定参数值（格式为“javascript:\<此处为恶意脚本>”）的 Web 页或报表服务器，并将此链接发送到引诱攻击中的其他人。  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>减少已发布报表或文档中的超链接脚本注入攻击  
 报表可以在报表项或报表项一部分的 Action 属性的值中包含嵌入的超链接。 在处理报表时，可将超链接绑定到从外部数据源检索的数据。 如果恶意用户修改基础数据，则超链接可能受到脚本攻击危害。 如果用户单击已发布或导出的报表中的链接，则可能会运行恶意脚本。  
  
 若要降低报表中包含无意中运行恶意脚本的链接的风险，请仅将超链接绑定到来自可信来源的数据。 验证查询结果中的数据和将数据绑定到超链接的表达式没有创建可被用来进行攻击的链接。 例如，不要将超链接基于连接多个数据集字段中的数据的表达式。 如有必要，浏览到此报表，然后使用“查看源”以检查可疑脚本和 URL。  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>减少参数化报表中的 SQL 注入攻击  
 包含类型参数的任何报表中`String`请务必使用可用值列表 （也称为有效值列表），并确保任何运行该报表的用户具有只需在报告中查看数据的权限。 定义 `String` 类型的参数时，系统将向用户显示一个可以使用任何值的文本框。 可用值列表限制可以输入的值。 如果报表参数与查询参数关联，但您没有使用可用值列表，则报表用户可能会在文本框中键入 SQL 语法，从而导致报表和服务器容易受到 SQL 注入攻击。 如果用户有足够的权限执行新的 SQL 语句，则可能在服务器上产生意外结果。  
  
 如果报表参数与查询参数无关，并且参数值包含在报表中，则报表用户可以在参数值中键入表达式语法或 URL，并将报表呈现为 Excel 或 HTML 格式。 如果其他用户查看报表并单击呈现的参数内容，则用户可能会无意中执行恶意脚本或链接。  
  
 若要降低无意中运行恶意脚本的风险，请仅从可信来源打开呈现的报表。  
  
> [!NOTE]  
>  在早期版本的文档中，包括以表达式形式创建动态查询的示例。 此类型的查询会产生 SQL 注入攻击漏洞，因而建议不要使用这类查询。  
  
## <a name="securing-confidential-reports"></a>保护机密报表  
 对于包含机密信息的报表，应通过要求用户在访问敏感数据时提供凭据，在数据访问级别上保护这些报表。 有关详细信息，请参阅[为报表数据源指定凭据和连接信息](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) 您也可以对文件夹进行保护，以便只有授权用户才能访问文件夹。 有关详细信息，请参阅 [保护文件](secure-folders.md)。  
  
## <a name="see-also"></a>请参阅  
 (create-and-manage-role-assignments.md)   
 [配置报表生成器访问权限](../report-server/configure-report-builder-access.md)   
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)   
 [保护共享数据源项](secure-shared-data-source-items.md)   
 [在 Reporting Services 数据源中存储凭据](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
