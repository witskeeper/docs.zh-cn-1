---
title: LoggingLevelEnum 枚举
ms.date: 03/30/2017
api_name:
- LoggingLevelEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LoggingLevelEnum
helpviewer_keywords:
- LoggingLevelEnum enumeration [.NET Framework debugging]
ms.assetid: 09daac08-005a-46b2-beab-408d0820c5e5
topic_type:
- apiref
ms.openlocfilehash: 01e1eafd9955a0876f77e34eb73c2a3fc6d815c2
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73139205"
---
# <a name="logginglevelenum-enumeration"></a>LoggingLevelEnum 枚举
指示在托管线程记录事件时写入事件日志的描述性消息的严重级别。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum LoggingLevelEnum {  
    LTraceLevel0 = 0,  
    LTraceLevel1,  
    LTraceLevel2,  
    LTraceLevel3,  
    LTraceLevel4,  
    LStatusLevel0 = 20,  
    LStatusLevel1,  
    LStatusLevel2,  
    LStatusLevel3,  
    LStatusLevel4,  
    LWarningLevel = 40,  
    LErrorLevel = 50,  
    LPanicLevel = 100  
} LoggingLevelEnum;  
```  
  
## <a name="members"></a>Members  
  
|成员|描述|  
|------------|-----------------|  
|`LTraceLevel0`|消息为跟踪级别0。|  
|`LTraceLevel1`|消息为跟踪级别1。|  
|`LTraceLevel2`|消息为跟踪级别2。|  
|`LTraceLevel3`|消息为跟踪级别3。|  
|`LTraceLevel4`|消息为跟踪级别4。|  
|`LStatusLevel0`|消息为状态级别0。|  
|`LStatusLevel1`|消息为状态级别1。|  
|`LStatusLevel2`|消息为状态等级2。|  
|`LStatusLevel3`|消息为状态级别3。|  
|`LStatusLevel4`|消息为状态等级4。|  
|`LWarningLevel`|消息为警告等级。|  
|`LErrorLevel`|消息为错误级别。|  
|`LPanicLevel`|消息是一个紧急级别。|  
  
## <a name="remarks"></a>备注  
 公共语言运行时（CLR）调用[ICorDebugManagedCallback：： LogMessage](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-logmessage-method.md)方法来通知调试器，托管线程已记录事件。 CLR 传递一个 `LoggingLevelEnum` 枚举的值，以指示托管线程写入事件日志的消息的严重性级别。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.EventLog>
- [调试枚举](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
