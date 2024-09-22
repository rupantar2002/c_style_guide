<!-- ## <u>**C NAMING CONVENTIONS**</u> -->

# C Style Guide

&nbsp;

> ### **TABLE OF CONTENTS**

1.  [Indentation](#indentation)
2.  [File Name](#file-name)
3.  [Header Files](#header-files)
4.  [Include Order](#include-order)
5.  [Macros](#macros)
6.  [Variables](#variables)
7.  [Enumerations](#enumerations)
8.  [Structures And Unions](#structures-and-unions)
9.  [Typedefs](#typedefs)
10. [Functions](#functions)
11. [Best Practices](#best-practices)

> ### **INDENTATION**

1.  Avoid using `tabs` and use `spaces`
2.  Convert `tabs` to `spaces`
3.  Make `tabsize` to `4 spaces`

> ### **FILE NAME**

1.  All lower case with all the words separated by underscore.

    <u>**Example :**</u> `my_file.x` , .x = file extension.

> ### **HEADER FILES**

1.  Files with `.h` extension is a header file .

    <u>**Example :**</u> `app_log.h`

2.  Always add `Header Guard` first.

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
2. `Other Library Headers`
3. `Project Specific Headers`

   <u>**Example :**</u> `app.h`.

   ```c
   #ifndef __APP_H__
   #define __APP_H__

   #include <stdint.h> // standard library
   #include <GLFW/glfw.h> // Other library
   #include <app_log.h> // project base library

   /* code area */

   #endif //__APP_LOG_H__
   ```

   <u>**Example :**</u> `app.c`.

   ```c
   #include <string.h> // standard library
   #include <glad.h> // Other library
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

    #define PH_SENSOR_DEVICE_VENDOR_ID "V_123"

    ```

3.  Instead of writing full name `first initials` or a `acronym` can be used but `name should be consistant in the module or package` and `should be descriptive`.

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
2.  Variable name must be in `lowerCamelCase` or `snake_case(Not Recomanded)`.
3.  Variable names must obey their `prefix`.

    ### Variable Prefix

    - `p` - For Pointer `int *pInteger = NULL`
    - `g` - For Global `static int gInteger = 0`
    - `pg` - For Global Pointer `static int *pgInteger = NULL`

4.  Variables declare and defined in `source files` i.e ` (.c files)` generaly considered as `private` .

5.  `Global variables` are private and must be declared as `static`.

6.  `Constant variables` must be writen in `CAPITAL_CASE`.

7.  `Constant variables` must be declared `before Other varibales` and should be `static`.

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
    ````

> ### **ENUMERATIONS**

1.  Enum name must be `prefixed` by `file_name` separated by underscore( `_` ).
2.  Enum name must be in `PascalCase` .
3.  Enum `elements` must be all `CAPITAL_CASE`.
4.  Enum `elements name` must be `prefixed` by `file_name` followed by `enum_name` all separated by underscore( `_` ) .

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

    // Typedef struct app_log_Context to app_log_Context_t
    typedef struct app_log_Context app_log_Context_t;

    typedef struct app_log_Context app_log_Ctx_t;
    ```

> ### **FUNCTIONS**

1.  Functions declared in `source files (.c files)` are `Private Functions`.
2.  Functions declared in `header files (.h files)` are `Public Functions`.
3.  `Public Function` name must be `prefixed` with `file_name` plus an underscore( `_` ).
4.  `Public Function` name must be in `PascalCase`.
5.  `Public Functions` must be `defined` in `source file`.
6.  `Private Function` name must be in `PascalCase`.
7.  `Private Function` must be declared `static`.
8.  `Private Functions` are defined `before` `Public Functions`.

    <u>**Example :**</u> `app_log.h`

    ```c
    // Public function declaration.
    void app_log_Init(void);

    // Public function declaration.
    void app_log_SetLevel(int level);

    ```

    <u>**Example :**</u> `app_log.c`

    ```c

    // Private function declaration.
    static void ClearLogBuffer(void);

    // Private function definition.
    static void ClearLogBuffer(void)
    {
        // code area
    }

    // Public function definition
    void app_log_Init(void)
    {
        // code area
    }

    // Public function definition
    void app_log_SetLevel(int level)
    {
        // code area
    }

    ```

> ### **BEST PRACTICES**

1.  Avoid `extern` as much as Possible.
2.  Avoid `goto` statements or use them carefully.
