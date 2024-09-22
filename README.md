<!-- ## <u>**C NAMING CONVENTIONS**</u> -->

# C Style Guide

&nbsp;

> ### **TABLE OF CONTENTS**

1.  [File Name](#file-name)
2.  [Header Files](#header-files)
3.  [Include Order](#include-order)
4.  [Macros](#macros)
5.  [Variables](#variables)
6.  [Enumarations](#enumerations)
7.  [Structures And Unions](#structures-and-unions)
8.  [Typedefs](#typedefs)
9.  [Functions](#functions)
10. [Generic](#generic)
11. [Notes](#notes)

&nbsp;

> ### **FILE NAME**

1.  All lower case with all the words seperated by underscore.

    <u>**Example :**</u> `my_file.x` , .x = file extention.

> ### **HEADER FILES**

1.  Files with `.h` extension is a header file .

    <u>**Example :**</u> `app_log.h`

2.  Allays add `Header Guard` first.

3.  Header guard must be in this format `__<FILE_NAME>_H__`

    <u>**Example :**</u> `app_log.h`

    ```c
    #ifndef __APP_LOG_H__
    #define __APP_LOG_H__

    /* code area */

    #endif //__APP_LOG_H__

    ```

> ### **INCLUDE ORDER**

1. `Standard Library Headers`
2. `Outher Library Headers`
3. `Project Specific Headers`

   <u>**Example :**</u> `app.h`.

   ```c
   #ifndef __APP_H__
   #define __APP_H__

   #include <stdint.h> // standard library
   #include <GLFW/glfw.h> // outher library
   #include <app_log.h> // project base library

   /* code area */

   #endif //__APP_LOG_H__
   ```

   <u>**Example :**</u> `app.c`.

   ```c
   #include <string.h> // standard library
   #include <glad.h> // outher library
   #include <app.h> // app header file

   /* code area */
   ```

> ### **MACROS**

1.  All `CAPITAL_CASE` with words `separated by` an underscore ( `_` ).
2.  Must be prefixed by the file name.

    <u>**Example :**</u> Considering file name as `ph_sensor.h`,

    ```c
    #define PH_SENSOR_DEVICE_ADDRESS (0x45)

    #define PH_SENSOR_DEVICE_CODE (123)

    #define PH_SENSOR_DEVICE_VENDOE_ID "V_123"

    ```

3.  Insted of writing full name `first initials` or a `acroname` can be used but `name should be consistant in the module or package` and `should be descriptive`.

    <u>**Example :**</u> Considering file name as `robot_arm.h`,

    ```c
    #define RA_JOINT_NUMBER (2)

    #define RA_MAXIMUM_ROTATION_ANGLE (150)

        or

    #define R_ARM_JOINT_NUMBER (2)

    #define R_ARM_MAXIMUM_ROTATION_ANGLE (150)

    ```

> ### **VARIABLES**

1.  Every variable name must be `self explanatory`.
2.  Variable name must be in `lowerCamelCase`.
3.  Variable names must obey their `prefix`.

    ### Variable Prefix

    - `p` - For Pointer `int *pInteger = NULL`
    - `g` - For Global `static int gInteger = 0`
    - `pg` - For Global Pointer `static int *pgInteger = NULL`

4.  Variables declare and defined in `source files` i.e ` (.c files)` generaly considered as `private` .

5.  `Global variables` are private and must be declared as `static`.

6.  `Constant variables` must be writen in `CAPITAL_CASE`.

7.  `Constant variables` must be declared `before outher varibales` and should be `static`.

8.  All `array names` must have `resonable suffix or prefix` , like `arr`, `table` or `matrix` to identify as array.

9.  `char array` or `char pointer` intended to be used as ASCII string must be `suffixed` or `prefixed` with `string` or `str`

10. Variable name should never start with a verb.

    <u>**Example :**</u>

    `runningDevice` **WRONG**

    `isDeviceRunning` **RIGHT**

    <u>**Example :**</u> `main.c`

    ````c

    static const char *MODULE_NAME_STR = "main"; /* Private constant variable */

    static int myGlobalVar = 0; /* Private global variable */

    static int *pgMyGlobalPtr = NULL; /* Private global pointer */

    static int gArrOfNumbers[]={1,2,3}; /* Private array of numbers */

    static const *gTableOfNames[]={"name","name","name"}; /* Private table of namess */

    static const *gIndentityMatrix3X3[][]={{1,0,0},{0,1,0},{0,0,1}}; /* Private matrix of numbers */

    static bool isDeviceReady = false; /* Private boolean variable */

    int main()
    {
        int myLocalVar = 0; /* local varibale */
        int arrOfNumbers[10]; /* local arry */

        char smapleString[]; /* chhar array */
        char *pSampleStr; /* chhar pointer */

        return 0;
    }
        ```
    ````

> ### **ENUMERATIONS**

1.  Enum name must be `prefixed` by `file_name`.
2.  Enum name must be in `PascalCase` .
3.  Enum `elements` must be all `CAPITAL_CASE`.
4.  Enum `elements` must be `prefixed` by `FILE_NAME` folowed by `ENUM_NAME`.

    <u>**Example :**</u>`app_log.h`

    ```c
    enum app_log_Level
    {
        APP_LOG_LEVEL_DEBUG=0,
        APP_LOG_LEVEL_INFO,
        APP_LOG_LEVEL_WARN,
        APP_LOG_LEVEL_ERROR,
        APP_LOG_LEVEL_MAX,
    };
    ```

> ### **STRUCTURES AND UNIONS**

1.  Structure or Union name must be `prefixed` by `file_name`.
2.  Structure or Union name must be in `PascalCase` .
3.  Structure or Union `elements` must be all `lowerCamelCase`.

    <u>**Example :**</u>`app_log.h`

    ```c
    struct app_log_Context
    {
        int globalLogLevel;
        char logBuffer[100];
    };

    union app_log_Value
    {
        int valueInt;
        float valueFloat;
        char valueStr;
    };
    ```

> ### **TYPEDEFS**

1.  Typedef name must be in `PascalCase`.
2.  Typedef name must be `prefixed` with `file_name` `if not private`.
3.  Typedef name must be `terminated with` `_t`

    <u>**Example :**</u> `app_log.h`

    ```c

    enum app_log_Level
    {
        APP_LOG_LEVEL_DEBUG=0,
        APP_LOG_LEVEL_INFO,
        APP_LOG_LEVEL_WARN,
        APP_LOG_LEVEL_ERROR,
        APP_LOG_LEVEL_MAX,
    };

    struct app_log_Context
    {
        int globalLogLevel;
        char logBuffer[100];
    };

    // Typedef an enum to app_log_Status_t
    typedef enum
    {
        APP_LOG_STATUS_OK=0,
        APP_LOG_STATUS_ERROR,
    }app_log_Status_t;

    // Typedef enum app_log_Level to app_log_Level_t
    typedef enum app_log_Level app_log_Level_t;

    // Typedef struct app_log_Context to app_log_Contex_t
    typedef struct app_log_Context app_log_Contex_t;


    typedef struct app_log_Context app_log_Ctx_t;
    ```

> ### **FUNCTIONS**

1. Functions declared in `source files` are `Private Functions`.
2. Functions declared in `header files` are `Public Functions`.
3. `Public Function` name must be `prefixed` with `file_name` plus an underscore( `_` ).
3. `Public Function` name must be in `PascalCase`.
3. `Public Functions` must be `defined` in `source file`.
4. `Private Function` name must be in `PascalCase`.
5. `Private Function` must be declared `static`.
6. `Private Functions` are defined `before` `Public Functions`.

> ### **PRIVATE FUNCTIONS**

1.  These functions should be strictly defined and declared in the source file only.
2.  Function name must contain a verb, preferably start with verb.
3.  Function name must be in upper camel case (Pascal Case)

    <u>**Example :**</u> `UpperCamelCase`

4.  Must be declared as static.
5.  File name prefixing should not be used.

> ### **PUBLIC FUNCTIONS**

1.  Function name must contain a verb, preferably start with verb.
2.  Function name must be in upper camel case (Pascal Case)
3.  Must be prefixed with file name.
4.  File name and function name should be seperated using an underscore.

    <u>**Example :**</u>

    A function inside a file `app_sensor.h` can be `app_sensor_GetSensorData()`

5.  Function name might be suffixed with their return type.`*`.

    - Type uint32*t: use suffix *`_ul`\_.
    - Type uint16*t: use suffix *`_us`\_.
    - Type uint8*t: use suffix *`_uc`\_.
    - Type void: use suffix _`_v`_.
    - Any other return type: use suffix _`_x`_.
    - Type pointer: use suffix _`_p`_ in addition to the above return type.

> ### **GENERIC**

This are to be followed for every namings, unless specified

1. Never use `__ or _` **prefix** for variables/functions/macros/types. This is reserved for C language itself

> ### **NOTES**

`*` **NOT MANDATORY**
