---
title: gcManagedToUnmanaged MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GcManagedToUnmanaged MDA
- GC managed to unmanaged
- transitioning threads managed to unmanaged code
- threading [.NET Framework], garbage collection
- managed to unmanaged garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
ms.assetid: 7417f837-805e-4fed-a430-ca919c8421dc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: afc0fd47e51723a7b3ba1b07dffc49260f88917d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052773"
---
# <a name="gcmanagedtounmanaged-mda"></a>gcManagedToUnmanaged MDA
每当线程从托管代码转换到非托管代码时，`gcManagedToUnmanaged` 托管调试助手 (MDA) 都会引起垃圾回收。  
  
## <a name="symptoms"></a>症状  
 当尝试使用已向 COM 公开的托管的对象时，非托管的用户组件会引发访问冲突。 COM 对象显示为已发布。 访问冲突具有不确定性。  
  
## <a name="cause"></a>原因  
 如果非托管组件未对托管的 COM 对象执行正确的引用计数，则当非托管组件仍拥有对象的引用时，运行时可能收集已向 COM 公开的托管对象。 运行时在垃圾回收期间调用 <xref:System.Runtime.InteropServices.Marshal.Release%2A>，因此如果用户组件在垃圾回收发生前使用对象，则不回收此对象。 这就造成了不确定性。  
  
## <a name="resolution"></a>解决方法  
 启用此助手可缩短对象符合回收条件时和调用 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 时的时间间隔，从而有助于跟踪首先尝试访问回收对象的非托管组件。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 每当线程从托管代码转换到非托管代码时，都会引起垃圾回收。  
  
## <a name="output"></a>Output  
 此 MDA 不会产生任何输出。  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcManagedToUnmanaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [使用托管调试助手诊断错误](diagnosing-errors-with-managed-debugging-assistants.md)
- [互操作封送处理](../interop/interop-marshaling.md)
- [gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)
