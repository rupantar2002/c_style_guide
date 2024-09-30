# C Style Guide

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
11. [Documentation and Commenting](#documentation-and-commenting)
    1. [Files](#commenting-files)
    2. [Macros](#commenting-macros)
    3. [Structures and Unions](#commenting-structures-and-unions)
    4. [Enums](#commenting-enums)
    5. [Typedefs](#commenting-typedefs)
    6. [Functions](#commenting-functions)
    7. [Variables](#commenting-variables)
    8. [Outher](#inline-comments)

> ### **INDENTATION**

1.  Avoid using tabs, `always use spaces`.
2.  Convert all `tabs to spaces`.
3.  Set `tab size` to `4 spaces`.

> ### **FILE NAME**

1.  File names should be `lowercase`, with words separated by underscores (`_`).

    <u>**Example :**</u> `my_file.x` , .x = file extension.

> ### **HEADER FILES**

1.  Files with the `.h` extension are header files.

    <u>**Example :**</u> `app_log.h`

2.  Always start header files with a `header guard`.
3.  Header guards should follow the format: `__FILE_NAME_H__`.

    <u>**Example :**</u> `app_log.h`

    ```c
    #ifndef __APP_LOG_H__
    #define __APP_LOG_H__

    /* code area */

    #endif //__APP_LOG_H__

    ```

> ### **INCLUDE ORDER**

1. Headers should be included in this order: `standard library` headers, `external library` headers, then `project library` headers.

   <u>**Example :**</u> `app.h`.

   ```c
   #ifndef __APP_H__
   #define __APP_H__

   #include <stdint.h> // standard library
   #include <GLFW/glfw.h> // external library
   #include <app_log.h> // project library

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

1.  All `CAPITAL_CASE` with words separated by an underscore (`_`).
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

8.  All `array names` must have resonable `suffix or prefix` , like `arr`, `table` or `matrix` to identify as array.

9.  `char array` or `char pointer` intended to be used as ASCII string must be `suffixed` or `prefixed` with `string` or `str`

10. Variable name should never start with a verb.

    <u>**Example :**</u>

    `runningDevice` **WRONG**

    `isDeviceRunning` **RIGHT**

    <u>**Example :**</u> `main.c`

    ```c

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

> ### **ENUMERATIONS**

1.  Enum name must be `prefixed` by `file_name` separated by underscore(`_`).
2.  Enum name must be in `PascalCase` .
3.  Enum `constants` must be all `CAPITAL_CASE`.
4.  Enum `constants` must be `prefixed` by `FILE_NAME` followed by `ENUM_NAME` all separated by underscore(`_`) .

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
        char valueStr[4];
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
9.  Function name should never start with a verb.

    <u>**Example :**</u>

    `DeviceRunning()` **WRONG**

    `IsDeviceRunning()` **RIGHT**

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

> ### **DOCUMENTATION AND COMMENTING**

- This guide recommands `Doxygen` for documentation and commenting.

- Example of doxygen `comment block`

  ```c
  /**
  *
  *
  */
  ```

- Example of doxygen `inline comment`

  ```c
  /**< description here */
  ```

- ## Annotations
  - `@file` Describes the contents of a file.
  - `@brief` Short summary of the construct (functions, macros, etc.).
  - `@param` Documents function parameters.
  - `@return` Documents the return value of functions.
  - `@struct` Describes structures and their members.
  - `@var` Documents members of structures or unions.
  - `@enum` Describes an enum type.
  - `@def` Documents macros.
  - `@typedef` Documents typedefs.
  - `@ingroup` Groups functions, variables, or types into modules or logical sections.
  - `@note` Adds important notes.
  - `@warning` Highlights critical warnings.
  - `@todo` Marks areas that need further development.
  - `@deprecated` Marks code as obsolete or not recommended for use.
  - `@example` Provides examples of how to use code constructs.
  - `@code` and `@endcode` Documents inline code examples.

1. ### Commenting Files

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
   * @file app_log.h
   * @brief Provides logging functionalities for the application.
   *
   * This file contains functions and structures to manage logs
   * within the application, including setting log levels.
   */

   #ifndef __APP_LOG_H__
   #define __APP_LOG_H__

   /* code area */

   #endif //__APP_LOG_H__
   ```

2. ### Commenting Macros

   <u>**Example :**</u> `ph_sensor.h`

   ```c
   /**
    * @brief Defines the device address for the pH sensor.
    *
    * This macro holds the I2C address used to communicate with the pH sensor.
    */
   #define PH_SENSOR_DEVICE_ADDRESS (0x45)
   ```

   ### or

   ```c
   #define PH_SENSOR_DEVICE_CODE (123) /**< Defines ph sensor device code */
   ```

3. ### Commenting Structures and Unions

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
    * @brief Holds the logging context for the application.
    *
    * This structure contains the global log level and a buffer
    * to hold log messages temporarily.
    */
   struct  app_log_Context{
       int globalLogLevel;    /**< Global log level for the application. */
       char logBuffer[100];   /**< Buffer to store log messages. */
   } ;

   /**
    * @brief Holds the log value.
    *
    * This union contains the log value.
    */
   union app_log_Value
   {
      int valueInt; /**< Integer value. */
      float valueFloat; /**< Fraction value. */
      char valueStr[4]; /**< String value. */
   };


   /**
    * @brief Holds the logging context for the application.
    *
    * This structure contains the global log level and a buffer
    * to hold log messages temporarily.
    */
   typedef struct {
       int globalLogLevel;    /**< Global log level for the application. */
       char logBuffer[100];   /**< Buffer to store log messages. */
   } app_log_Context_t;
   ```

4. ### Commenting Enums

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
    * @brief Defines log levels for the application.
    *
    * These enum values represent different levels of logging
    * verbosity in the system.
    */
   typedef enum {
       APP_LOG_LEVEL_DEBUG = 0,  /**< Detailed debug messages. */
       APP_LOG_LEVEL_INFO,       /**< Informational messages. */
       APP_LOG_LEVEL_WARN,       /**< Warnings about potential issues. */
       APP_LOG_LEVEL_ERROR       /**< Critical errors that need attention. */
    } app_log_Level_t;
   ```

5. ### Commenting Typedefs

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
    * @brief Typedef for the logging status codes.
    *
    * This typedef makes it easier to reference the log status codes
    * defined in the app_log_Status enum.
    */
   typedef enum app_log_Status app_log_Status_t;
   ```

6. ### Commenting Functions

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
    * @brief Initializes the logging system.
    *
    * This function sets up the logging system and prepares it for use.
    * It should be called at the start of the application.
    *
    * @param level Initial log level to be set (0 = Debug, 1 = Info, etc.).
    * @return 0 if initialization was successful, -1 otherwise.
    */
   int app_log_Init(int level);
   ```

7. ### Commenting Variables

   <u>**Example :**</u> `app_log.c`

   ```c
   /**
    * @brief Holds the current log level for the application.
    *
    * This variable controls the verbosity of log messages
    * in the system. Lower levels produce more detailed logs.
    */
   int globalLogLevel;
   ```

   ### or

   ```c
   int globalLogLevel; /**< Holds the current log level for the application. */
   ```

8. ### Inline Comments

   <u>**Example :**</u> `app_log.h`

   ```c
   int app_log_SetLevel(int level) {
       if (level < APP_LOG_LEVEL_DEBUG || level > APP_LOG_LEVEL_ERROR) {
           return -1; /**< Invalid log level. */
    }

    // Set the global log level to the provided value.
    globalLogLevel = level;

    return 0; /**< Successfully set the log level. */
   }
   ```

9. ### Modules or Groups (Files, Functions,Structures etc.)

   <u>**Example :**</u> `app_log.h`

   ```c
   /**
    * @defgroup Logging Logging Module
    * @file app_log.h
    * @brief Provides logging functionality for the application.
    *
    */

   #ifndef __APP_LOG_H__
   #define __APP_LOG_H__

   /**
    * @defgroup Logging Logging Module
    * @brief Holds the logging context for the application.
    *
    */
    typedef struct {
       int globalLogLevel;    /**< Global log level for the application. */
       char logBuffer[100];   /**< Buffer to store log messages. */
    } app_log_Context_t;


   /**
    * @defgroup Logging Logging Module.
    * @brief Initializes the logging system.
    * @param level Initial log level to be set (0 = Debug, 1 = Info, etc.).
    * @return 0 if initialization was successful, -1 otherwise.
    */
   int app_log_Init(int level);

   ```

10. ### Todo , Warnings , Note and Deprecated

    <u>**Example :**</u> `app_log.h`

    ```c
    /**
     * @brief Resets the logging system.
     *
     * @todo Add error handling for memory allocation failures.
     */
    void app_log_Reset(void);

    /**
     * @brief Clear's log buffer.
     *
     * @warning Clears all logs; this action is irreversible.
     */
    void app_log_Clear(void);

    /**
     * @note This function must be called before any log is written.
     */
    void app_log_Init(void);

    /**
     * @deprecated Use app_log_SetLevel() instead.
     */
    void app_log_SetLoggingLevel(int level);

    ```

11. ### Example Section

    <u>**Example :**</u> `app_log.h`

    ```c
    /**
     * @example log_example.c
     *
     * This is an example of how to use the logging system.
     *
     * @code
     *   app_log_Init(APP_LOG_LEVEL_INFO);
     *   app_log_SetLevel(APP_LOG_LEVEL_DEBUG);
     * @endcode
     */
    ```
