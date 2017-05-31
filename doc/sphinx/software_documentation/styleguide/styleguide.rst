.. include:: ../../macros.rst



.. _software_styleguide:

====================
Software Style Guide
====================

.. highlight:: C

Introduction
------------

This document shows the codings guidelines used in |foxbms|.


Structure of Modules, Files and Functions
-----------------------------------------

General
~~~~~~~

Every file shall have a header, using |doxygen|. The file header has to be above all other commentary, code or includes. The file header includes two splitted parts, both using |doxygen|. The first part includes:

 - @copyright
 - <License>

The second part includes:

 - @file    
 - @author  
 - @date    
 - @ingroup 
 - @prefix  
 - @brief   
 - followed by an extensive description of the module/file

.. code-block:: C

    /**
     *
     * @copyright &copy; 2010 - 2017, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. All rights reserved.
     *
     * BSD 3-Clause License
     * Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
     * 1.  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
     * 2.  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
     * 3.  Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
     *
     * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
     *
     * We kindly request you to use one or more of the following phrases to refer to foxBMS in your hardware, software, documentation or advertising materials:
     *
     * &Prime;This product uses parts of foxBMS&reg;&Prime;
     *
     * &Prime;This product includes parts of foxBMS&reg;&Prime;
     *
     * &Prime;This product is derived from foxBMS&reg;&Prime;
     *
     */

    /**
     * @file    xyz.[c|h]
     * @author  foxBMS Team
     * @date    [xx.xx.xxxx] (date of creation)
     * @ingroup [xxXX]
     * @prefix  [xxXX]
     *
     * @brief   [xx xx xx]
     *
     * aaaa
     *
     */

Header Files
~~~~~~~~~~~~

All header files need a #define guard against multiple inclusions using the following style:

.. code-block:: C

   #ifndef FILE_H_
   #define FILE_H_
   #endif // FILE_H_


- All public functions have to be defined as ``extern`` in the header file. The API/doxygen to these public functions also have to be in the header. All functions need to use module-prefix in upper case.
- All public varibales have to be defined as ``extern`` in the header file. All public variables need to use module-prefix in lower case.

.. code-block:: C

   /**
    * important variable
    */
   extern <type> <prefix>_variableName;
   
   /**
    * @brief   brief description of the function
    *
    * long description
    * long description
    * long description
    
    * @param   abc
    *
    * @return  xyz
    */
   extern <type> <PREFIX>_FunctionName(<type> abc);


Sources Files
~~~~~~~~~~~~~

- All private functions have to be defined as ``static`` in the source file. The API/doxygen to these private functions also have to be in the sources file. All functions need to use module-prefix in upper case.
- All private varibales have to be defined as ``static`` in the source file. All private variables need to use module-prefix in lower case.

.. code-block:: C

   /**
    * important variable
    */
   static <type> <prefix>_variableName;
   
   /**
    * @brief   brief description of the function
    *
    * long description
    * long description
    * long description
    
    * @param   abc
    *
    * @return  xyz
    */
   static <type> <PREFIX>_FunctionName(<type> abc);


Variables and Functions
~~~~~~~~~~~~~~~~~~~~~~~

+--------+-------------+---------+--------------+
| module | Files       | acronym | example      |
+--------+-------------+---------+--------------+
| spi    | spi.c       | SPI     | SPI_Init()   |
|        | spi.h       |         | spi_state    |
|        | spi_cfg.c   |         | SPI_MACRO    |
|        | spi_cfg.h   |         |              |
+--------+-------------+---------+--------------+

Typedefs, Enums, Structs
~~~~~~~~~~~~~~~~~~~~~~~~

- The ‘_’ can (but need not) be used to separate words in the names
- They mus start with the module prefix.
- all typedef struct definitions should have name suffixed by “_s”
- all typedef enum definitions should have name suffixed by “_e”
- all typedef enums must be in upper cases
- all enumeration, function and struct names should be concatenation of words where first letter of each word should start with capital letter.

Example ``enum``:

.. code-block:: C

   typedef enum FES_FATAL_ERROR_SOURCE {
       FES_UNDEFINED                     = 0,   /*!< description  /*
       FES_MAIN                          = 1,   /*!< description  /*
       FES_CHECK_COPY_OF_SYSTEM_LIMITS   = 2,   /*!< description  /*
       FES_STATE_VOTER_FAST              = 3,   /*!< description  /*
       FES_STATE_VOTER_SLOW              = 4,   /*!< description  /*
   } FES_FATAL_ERROR_SOURCE_e;


Example ``struct``:

.. code-block:: C

   typedef struct BmsAlgo_Sof_ConfigType {
       double i_dischamax_cont;     /*!< Unit 10mA       /*
       double i_chargemax_cont;     /*!< Unit 10mA       /* 
       double i_limphome;           /*!< description     /*
       double cutoff_tlow_discha;   /*!< Unit 1 Celsius  /*
       double limit_tlow_discha;    /*!< Unit 1 Celsius  /*
   } BmsAlgo_Sof_ConfigType_s;


Horizontal Whitespace
~~~~~~~~~~~~~~~~~~~~~

To indent code blocks, 4 spaces are used instead of tabs.

Complete Example
----------------

The following module xyz shows a complete example how to follow the coding guidelines.

xyz_cfg.h
~~~~~~~~~

.. code-block:: C

   /**
    *
    * @copyright &copy; 2010 - 2017, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. All rights reserved.
    *
    * BSD 3-Clause License
    * Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
    * 1.  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
    * 2.  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
    * 3.  Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
    * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
    *
    * We kindly request you to use one or more of the following phrases to refer to foxBMS in your hardware, software, documentation or advertising materials:
    *
    * &Prime;This product uses parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product includes parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product is derived from foxBMS&reg;&Prime;
    *
    */
   
   /**
    * @file    xyz_cfg.h
    * @author  the fox
    * @date    xx.xx.xxxx
    * @ingroup DRIVERS_CONF
    * @prefix  XYZ
    *
    * @brief   Header for the configuration xyz
    *
    * This file defines all needed macros to map the xyz and a lot more
    *
    */
   
   #ifndef XYZ_CFG_H_
   #define XYZ_CFG_H_
   
   /*================== Includes =============================================*/
   #include "general.h"
   #include "furthermore.h"
   /*================== Macros and Definitions ===============================*/
   
   /**
    * This define does this and that
    */
   #define XYZ_THIS_AND_THAT_MACRO (43)
   
   
   /*fox
    * this is a Foxygen configurable macro
    * @var     this macro is used for this
    * @type    int
    * @default 100
    * @valid   [90,110]
    * @units   ms
    * @level   user
    * @group   XYZ
    */
   #define XYZ_FOXYGEN_MACRO (100)
   
   /*================== Constant and Variable Definitions ====================*/
   /**
    * Symbolic names for some states
    */
   typedef enum XYZ_SWITCH {
       XYZ_SWITCH_OFF     = 0,   /*!< switch off         --> switch is open         */
       XYZ_SWITCH_ON      = 1,   /*!< switch on          --> switch is closed       */
       XYZ_SWITCH_UNDEF   = 2,   /*!< switch undefined   --> switch state not known */
   } XYZ_SWITCH_e;
   

   typedef struct XYZ_STATE {
       boolean value;         /*!< value that means this */
       uint32_t timestamp;    /*!< and has a timestamp   */
   } XYZ_STATE_s;

   extern const uint8_t xyz_module_cfg_length;
   extern uint8_t xyz_counter;
   
   /*================== Function Prototypes ==================================*/

   /*================== Function Implementations =============================*/

   #endif /* XYZ_CFG_H_ */

xyz_cfg.c
~~~~~~~~~

.. code-block:: C

   /**
    *
    * @copyright &copy; 2010 - 2017, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. All rights reserved.
    *
    * BSD 3-Clause License
    * Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
    * 1.  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
    * 2.  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
    * 3.  Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
    * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
    *
    * We kindly request you to use one or more of the following phrases to refer to foxBMS in your hardware, software, documentation or advertising materials:
    *
    * &Prime;This product uses parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product includes parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product is derived from foxBMS&reg;&Prime;
    *
    */
   
   /**
    * @file    xyz_cfg.c
    * @author  the fox
    * @date    xx.xx.xxxx
    * @ingroup DRIVERS_CONF
    * @prefix  XYZ
    *
    * @brief   Sorces for the configuration xyz
    *
    * This file defines important things for the driver!
    *
    */
   
   /*================== Includes =============================================*/
   #include "xyz_cfg.h"

   /*================== Macros and Definitions ===============================*/

   /*================== Constant and Variable Definitions=====================*/

   XYZ_STATE_s xyz_state_1 = {
           1, 1
   };

   uint8_t xyz_module_cfg_length = XYZ_THIS_AND_THAT_MACRO;
   uint8_t xyz_counter = 0;
   
   /*================== Function Prototypes ==================================*/

   /*================== Function Implementations =============================*/


xyz.h
~~~~~

.. code-block:: C

   /**
    *
    * @copyright &copy; 2010 - 2017, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. All rights reserved.
    *
    * BSD 3-Clause License
    * Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
    * 1.  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
    * 2.  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
    * 3.  Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
    * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
    *
    * We kindly request you to use one or more of the following phrases to refer to foxBMS in your hardware, software, documentation or advertising materials:
    *
    * &Prime;This product uses parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product includes parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product is derived from foxBMS&reg;&Prime;
    *
    */
   
   /**
    * @file    xyz.h
    * @author  the fox
    * @date    xx.xx.xxx
    * @ingroup DRIVERS
    * @prefix  XYZ
    *
    * @brief   Header for the driver for the contactors
    *
    * This file makes the declaration of the public functions of the contactor
    * driver.
    *
    */
   
   #ifndef XYZ_H_
   #define XYZ_H_
   
   /*================== Includes =============================================*/
   #include "xyz_cfg.h"

   /*================== Macros and Definitions ===============================*/

   /*================== Constant and Variable Definitions=====================*/

   /*================== Function Prototypes ==================================*

   /**
    * @brief   does this and that
    *
    * but this has to be described way better with a longer text
    *
    * @return  void
    */
   extern uint8_t XYZ_Function(void);
   
   /*================== Function Implementations =============================*/
   #endif // XYZ_H_

xyz.c
~~~~~

.. code-block:: C

   /**
    *
    * @copyright &copy; 2010 - 2017, Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V. All rights reserved.
    *
    * BSD 3-Clause License
    * Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:
    * 1.  Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
    * 2.  Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
    * 3.  Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.
    * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
    *
    * We kindly request you to use one or more of the following phrases to refer to foxBMS in your hardware, software, documentation or advertising materials:
    *
    * &Prime;This product uses parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product includes parts of foxBMS&reg;&Prime;
    *
    * &Prime;This product is derived from foxBMS&reg;&Prime;
    *
    */
   
   /**
    * @file    xyz.h
    * @author  the fox
    * @date    xx.xx.xxxx
    * @ingroup DRIVERS
    * @prefix  XYZ
    *
    * @brief   Driver for the thing
    *
    * This module is designed as a wrapper of the io-module, to easily handle
    * contactors. It allows an easy switching off the contactor state and
    * measuring the feedback and storing these data.
    * In case of opening the contactors under load an error entry is performed.
    *
    */
   
   /*================== Includes =============================================*/
   #include "xyz.h"
   #include "otherinclude.h"
   /*================== Macros and Definitions ===============================*/
   
   /*================== Constant and Variable Definitions=====================*/
   /**
    * locally used varibale with this and that
    */
   static uint8_t xyz_variablename = 1;
   
   /*================== Function Prototypes ==================================*/
   static uint8_t XYZ_LocalFunction(void);
    
   /*================== Function Implementations =============================*/
   
   /*================== Public functions======================================*/
   
   uint8_t XYZ_Function(void) {
      xyz_counter++;
      return 0; 
   }
   
   /*================== Static functions======================================*/
   
   /**
    * @brief   this and that
    *
    * long, long description
    *
    * @return  retVal
    */
   uint8_t XYZ_LocalFunction(void) {
      uint8_t abc = 1;
      abc++;
      return abc;
   }

   