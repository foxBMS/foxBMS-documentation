.. include:: ../../../macros.rst

.. _SYSCTRL:

==============
System Control
==============

.. highlight:: C

System Control (|mod_sysctrl|) handles states request from BMS Control (|mod_bmsctrl|) or error requests from the Diagnosis (|mod_diag|). It controls the operating modes of the BMS and the 
contactors according to the entered states.


Module Files
~~~~~~~~~~~~~~

Driver:
 - ``src\engine\syscontrol.c``
 - ``src\enginesyscontrol.h``
 
Driver Configuration:
 - ``src\engine\config\syscontrol_cfg.c``
 - ``src\engine\config\syscontrol_cfg.h``


Dependencies
~~~~~~~~~~~~

 - |mod_contactor|
 - |mod_database|
 - |mod_diag|


Statemachine of SYSCTRL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``SysControl`` is implemented as a state machine.
When starting up the system, ``SYSCTRL_Trigger()`` is called in ``OS_PostOSInit()`` with the intention to make  powerup- and selfchecks of the BMS and, finally, to enter the state ``STANDBY``. In this state the interlock switch is ON and all contactors are OFF. The system is ready for entering ``NORMAL`` state.
During system runtime  ``SysControl`` is periodically called from the engine task ``OS_TSK_Cyclic_10ms()`` to handle external state requests, control the state transitions and the contactors accordingly.

The states that may be required from an external module (higher level control unit) are ``POWER OFF``, ``STANDBY`` and ``NORMAL``.

:numref:`Fig. %s <sysctrl_figure1>` shows the organization of the Syscontrol statemachine.

.. _sysctrl_figure1:
.. figure:: syscontrol.png
   :width: 100 %

   System Control state machine

Description of the states
-------------------------

The main states of the statemachine are:

+-----------------------------------+-----------------------------------------------------------------------------------------------+
| State                             | Description                                                                                   |
+===================================+===============================================================================================+
| ``UNINITIALIZED``                 | Initial state at startup.                                                                     |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``INIT``                          | First state which will be entered after startup where startup checks are done,                |
|                                   | e.g. checking the operability ot the contactors.                                              |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``AWAKE``                         | Wake up state from sleep mode                                                                 |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``SLEEP``                         | Entering state to sleep mode (implementation optional)                                        |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``IDLE``                          | Idle state (ready for entering STANDBY state,interlock OFF, contactors OFF))                  |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``STANDBY``                       | Stanby state (ready for entering NORMAL state, interlock ON, contactors OFF)                  |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``NORMAL``                        | Main contactors are closed.                                                                   |
+-----------------------------------+-----------------------------------------------------------------------------------------------+
| ``ERROR``                         | Any kind of problem which is handled by switching off the interlock and contactors            |
|                                   |                                                                                               |
| ``PRECHARGE_ERROR``               | Opens all contactors but not the interlock.                                                   |
+-----------------------------------+-----------------------------------------------------------------------------------------------+


Procedure in State NORMAL
-------------------------

The state of the interlock line is continuously monitored in ``NORMAL`` state.
If the line is interrupted, the statemachine opens the interlock and contactor switches to be 
consisted with the hardware state.

Any exit from the NORMAL state will result in opening the contactors. 

When entering NORMAL state, the following procedure is performed:
The interlock switch is already closed (in STANDBY state)

1. close minus main contactor, then wait and go to 2

2. check if main minus contactor is closed

  1. if minus main contactor is closed: go to 3
  2. if minus main contactor open and timeout reached: exit to error state
  
3. close plus precharge contactor and wait and go to 4
4. check if plus precharge contactor is closed

  1. if plus precharge contactor is closed: go to 5
  2. if open and timeout reached: exit to error state
  
5. loop and check precharge end conditions (U diff < threshold, I < threshold)

  a. precharge end condition OK: close plus main contactor and wait and go to 6
  b. precharge end condition BUSY (means waiting): wait if timer has not elapsed, else go to error state
  
6. open plus precharge contactor and go to 7
7. check if plus main contactor is closed

  1. if plus main contactor is closed: go to 8
  2. if open and timeout reached: exit to error state
  
8. continuous check if main plus and main minus is closed

  1. if plus main or minus main contactor open: exit to error state
  2. if plus main and minus main contactor open closed: go to 8 (loop)

:numref:`Fig. %s <sysctrl_figure2>` shows the detailed sequence of the normal state of the Syscontrol statemachine.

.. _sysctrl_figure2:
.. figure:: sysctrl_detailednormal.png
   :width: 100 %

   Detailed view of SysControl state NORMAL

Configuration of SYSCTRL
~~~~~~~~~~~~~~~~~~~~~~~~

.. Default Configuration
.. ---------------------

The configuration of timeouts, thresholds etc. is done in ``syscontrol_cfg.h``. All configurations are accessible with |foxygen|. The macros of the contactor module are mapped to the macros of |mod_sysctrl|.


Usage
~~~~~

Initialization
--------------

The statemachine is initialized by ``SYSCTRL_Trigger()`` and the starting point of the syscontrol state machine is ``UNINITIALIZED``. In this state the contactor initialization is called, and checks if all contactors are open.

Functions
---------

``static void SYSCTRL_StateControl(void)`` performs the state transitions with all needed sub-steps between the states. It is important to know, that when entering an error state, the contactors are opened by using the macro ``SYSCTRL_ALL_CONTACTORS_OFF()``; Therefore, if the user adds additional error states, this macro should be used accordingly. For detailed description of the states, see |doxygen| documentation.
 