---
title: 如何：从 Windows 窗体 DomainUpDown 控件移除项
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DomainUpDown control [Windows Forms], removing items from
- spin button control [Windows Forms], removing items
ms.assetid: e70f5cbc-b497-41a9-975a-344c00e56ed2
ms.openlocfilehash: f56bc2b7b7b8a783ac298b220c83281f38da29da
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662354"
---
# <a name="how-to-remove-items-from-windows-forms-domainupdown-controls"></a>如何：从 Windows 窗体 DomainUpDown 控件移除项
可以从 Windows 窗体中移除项<xref:System.Windows.Forms.DomainUpDown>控件通过调用<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A>或<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A>方法的<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection>类。 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A>方法中删除特定项，而<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A>方法中移除的项按其位置。  
  
### <a name="to-remove-an-item"></a>若要删除项  
  
- 使用<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A>方法的<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection>类名称中删除项。  
  
    ```vb  
    DomainUpDown1.Items.Remove("noodles")  
    ```  
  
    ```csharp  
    domainUpDown1.Items.Remove("noodles");  
    ```  
  
    ```cpp  
    domainUpDown1->Items->Remove("noodles");  
    ```  
  
     或  
  
- 使用<xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A>方法中删除的项按其位置。  
  
    ```vb  
    ' Removes the first item in the list.  
    DomainUpDown1.Items.RemoveAt(0)  
    ```  
  
    ```csharp  
    // Removes the first item in the list.  
    domainUpDown1.Items.RemoveAt(0);  
    ```  
  
    ```cpp  
    // Removes the first item in the list.  
    domainUpDown1->Items->RemoveAt(0);  
    ```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.DomainUpDown>
- <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A?displayProperty=nameWithType>
- [DomainUpDown 控件](domainupdown-control-windows-forms.md)
- [DomainUpDown 控件概述](domainupdown-control-overview-windows-forms.md)
