project(
    'libcoren2g',
    'c',
    'cpp',
    version : '3.6.1',
    default_options : [
        'c_std=gnu99',
        'cpp_std=gnu++17',
        'board=TOOL1RR'
    ]
)

c_args = []
cpp_args = []

includes = [
    'src/',
]

sources = [
    'src/Atomic.cpp',
    'src/Cache.cpp',
    'src/CanDevice.cpp',
    'src/CoreIO.cpp',
    'src/Print.cpp',
    'src/SerialCDC_tusb.cpp',
    'src/Stream.cpp',
    'src/TinyUsbInterface.cpp',
    'src/UniqueIdBase.cpp'
]

if get_option('board') == 'TOOL1RR'
    includes += [
        'src/SAME5x_C21/SAME5x',
        'src/SAME5x_C21/SAME5x/hal/include',
        'src/SAME5x_C21/SAME5x/hal/utils/include',
        'src/SAME5x_C21/SAME5x/hri',
        'src/SAME5x_C21/SAME5x/Config',
        'src/atmel/SAME54_DFP/1.1.134/include',
        'src/arm/CMSIS/5.4.0/CMSIS/Core/Include'
    ]

    sources += [
        'src/SAME5x_C21/AnalogOut.cpp',
        'src/SAME5x_C21/AnalogOut.cpp',
        'src/SAME5x_C21/AsyncSerial.cpp',
        'src/SAME5x_C21/DmacManager.cpp',
        'src/SAME5x_C21/Flash.cpp',
        'src/SAME5x_C21/Interrupts.cpp',
        'src/SAME5x_C21/Serial.cpp',
        'src/SAME5x_C21/SAME5x/AnalogIn.cpp',
        'src/SAME5x_C21/SAME5x/Sdhc.cpp',
        'src/SAME5x_C21/SAME5x/SerialCDC.cpp',
        'src/SAME5x_C21/SAME5x/SimpleAnalogIn.cpp',
        'src/SAME5x_C21/SAME5x/Startup.cpp',
        'src/SAME5x_C21/SAME5x/hal/src/hal_atomic.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_flash.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_gpio.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_mac_async.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_rand_sync.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_sleep.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_usb_device.c',
        'src/SAME5x_C21/SAME5x/hal/src/hal_wdt.c',
        'src/SAME5x_C21/SAME5x/hal/utils/src/utils_assert.c',
        'src/SAME5x_C21/SAME5x/hal/utils/src/utils_event.c',
        'src/SAME5x_C21/SAME5x/hal/utils/src/utils_list.c',
        'src/SAME5x_C21/SAME5x/hpl/core/hpl_core_m4.c',
        'src/SAME5x_C21/SAME5x/hpl/gmac/hpl_gmac.c',
        'src/SAME5x_C21/SAME5x/hpl/nvmctrl/hpl_nvmctrl.c',
        'src/SAME5x_C21/SAME5x/hpl/usb/hpl_usb.c',
        'src/SAME5x_C21/SAME5x/hpl/wdt/hpl_wdt.c'
    ]

    c_args += [
        '-D__SAME54P20A__',
        '-Dnoexcept=',
        '-DSUPPORT_CAN=1',
        '-DSUPPORT_SDHC=0',
        '-DSUPPORT_USB=0',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fdata-sections',
        '-nostdlib',
        '-Wundef',
        '-Wdouble-promotion',
        '-Werror=return-type',
        '-Werror=implicit',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
    ]

    cpp_args += [
        '-D__SAME54P20A__',
        '-DSUPPORT_CAN=1',
        '-DSUPPORT_SDHC=0',
        '-DSUPPORT_USB=0',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fdata-sections',
        '-fno-threadsafe-statics',
        '-fno-rtti',
        '-fno-exceptions',
        '-nostdlib',
        '-Wundef',
        '-Wdouble-promotion',
        '-Werror=return-type',
        '-Wsuggest-override',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
        '-fstack-usage',
    ]
endif

libfreertos = subproject('libfreertos')
libfreertos_dep = libfreertos.get_variable('libfreertos_dep')

librrflibraries = subproject('librrflibraries')
librrflibraries_dep = librrflibraries.get_variable('librrflibraries_dep')

libcanlib = subproject('libcanlib')
libcanlib_dep = libcanlib.get_variable('libcanlib_dep')

libcoren2g = static_library(
    'coren2g',
    sources,
    include_directories : include_directories(includes),
    dependencies : [
        libfreertos_dep,
        librrflibraries_dep,
        libcanlib_dep,
    ],
    c_args : c_args,
    cpp_args : cpp_args
)

libcoren2g_dep = declare_dependency(
    include_directories : include_directories(includes),
    link_with : libcoren2g
)
