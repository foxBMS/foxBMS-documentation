.. -----------------------------------------------
.. General Documentation Macros
.. -----------------------------------------------
.. |foxbms| replace:: foxBMS
.. |foxconda| replace:: foxConda
.. |frontdesk| replace:: Front Desk
.. |foxygen| replace:: Foxygen
.. |LTC| replace:: LTC6804-1/LTC6811-1
.. |master| replace:: foxBMS Master Unit
.. |masters| replace:: foxBMS Master Units
.. |slave| replace:: foxBMS Slave Unit
.. |slaves| replace:: foxBMS Slave Units
.. |BMS-Master| replace:: BMS-Master board
.. |BMS-Extension| replace:: BMS-Extension board
.. |BMS-Interface| replace:: BMS-Interface board
.. |BMS-Slave| replace:: BMS-Slave board
.. |BMS-Slaves| replace:: BMS-Slave boards
.. |MCU0| replace:: MCU0
.. |MCU1| replace:: MCU1
.. |CAN0| replace:: CAN_0
.. |CAN1| replace:: CAN_1

.. -----------------------------------------------
.. Software Module Macros
.. -----------------------------------------------
.. |diag module| replace:: ``diag`` module
.. |contactor module| replace:: ``contactor`` module
.. |syscontrol module| replace:: ``syscontrol`` module
.. |bmsctrl module| replace:: ``bmsctrl`` module
.. |can module| replace:: ``can`` module
.. |cansignal module| replace:: ``can`` module
.. |io module| replace:: ``io`` module
.. |isoguard module| replace:: ``isoguard`` module
.. |primary archive| replace:: ``foxbms_primary-0-4-3.tar.gz``
.. |secondary archive| replace:: ``foxbms_secondary-0-4-3.tar.gz``
.. |installer archive| replace:: ``foxcondainstaller-0-4-3.exe``

.. -----------------------------------------------
.. Hardware-Software Quickcheck Macros
.. -----------------------------------------------
.. |eo| replace:: ``emergency off``
.. |il| replace:: ``interlock``
.. |pmc| replace:: ``plus main contactor``
.. |ppc| replace:: ``plus precharge contactor``
.. |mmc| replace:: ``minus main contactor``
.. |version| replace:: ``0.4.4``
.. |hear| replace:: *(H)*
.. |build| replace:: ``python Tools\waf-1.8.12 configure --check-c-compiler=gcc build``
.. |drive| replace:: Drive
.. |stdby| replace:: Standby

.. -----------------------------------------------
.. Variable Name Macros
.. -----------------------------------------------
.. |var_il| replace:: variable: ``cont_interlock_state``
.. |var_co| replace:: variable: ``cont_contactor_states``
.. |var_bkpsram_co| replace:: variable: struct ``bkpsram_ch_1`` member: ``contactors_count``
.. |var_sysctrl_st| replace:: variable ``sysctrl`` member: ``SYSCTRL_STATEMACH_e``

.. -----------------------------------------------
.. State Machine Macros
.. -----------------------------------------------
.. |req_drive| replace:: Request "Drive"-state via CAN
.. |req_stdby| replace:: Request "Standby"-state via CAN
.. -----------------------------------------------
