- FreeRTOSConfig.h: FreeRTOS的配置文件，通过配置定义宏定义
- Cortex-M内核使用8bit来配置优先级，但是STM32只使用了高4bit，数值越小，优先级越高。在往寄存器里面写数值配置的时候，是按照8bit来写的，所以真正写的时候需要经过转换，公式为：
`((priority<<(8-__NVIC_PRIO_BITS))&0xff)` 其中的priority就是我们配置的真正的优先级
- SysTick的优先级我们一般配置为最低，即0xf 。这样可以提高系统的实时响应能力，即其他的外部中断可以及时的得到响应。
- 用于配置STM32的特殊寄存器basepri寄存器的值，用于屏蔽中断，当大于basepri值的优先级的中断将被全部屏蔽。basepri只有4bit有效，默认只为0，即全部中断都没有被屏蔽.