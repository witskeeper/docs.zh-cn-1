---
title: 缓解：路径冒号检查
ms.date: 03/30/2017
ms.assetid: a0bb52de-d279-419d-8f23-4b12d1a3f36e
ms.openlocfilehash: e88643fea3bd507289436f41880a2de34117884f
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2019
ms.locfileid: "73457897"
---
# <a name="mitigation-path-colon-checks"></a>缓解：路径冒号检查
自面向 .NET Framework 4.6.2 的应用起，为了支持以前不受支持的路径，执行了大量更改（无论是在长度方面还是在格式方面）。 特别是，能够更加准确地检查驱动器分隔符语法（冒号）的用法是否正确。  
  
## <a name="impact"></a>影响  
 这些更改阻止了 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> 和 <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 方法以前支持的一些 URI 路径。  
  
## <a name="mitigation"></a>缓解  
 若要解决 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> 和 <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 方法不再支持以前可接受的路径的问题，可执行以下操作：  
  
- 从 URL 中手动删除协议。 例如，从 URL 中删除 `file://`。  
  
- 将 URI 传递给 <xref:System.Uri> 构造函数，并检索 <xref:System.Uri.LocalPath%2A?displayProperty=nameWithType> 属性的值。  
  
- 通过将 `Switch.System.IO.UseLegacyPathHandling`<xref:System.AppContext> 开关设置为 `true` 来选择禁用新的路径规范化。  
  
    ```xml  
    <runtime>  
        <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
    </runtime>  
    ```  
  
## <a name="see-also"></a>请参阅

- [应用程序兼容性](application-compatibility.md)
