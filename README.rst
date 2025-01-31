.. zephyr:code-sample:: ipc-static-vrings
   :name: IPC service: static vrings backend
   :relevant-api: ipc

   Send messages between two cores using the IPC service and static vrings backend.

Overview
********

This application demonstrates how to use IPC Service and the static vrings
backend with Zephyr. It is designed to demonstrate how to integrate it with
Zephyr both from a build perspective and code. There is an extra ipc instance that 
sends data back from one core to the other, highlighting that you swap the return 
path. The second transceive ipc task runs at a delay that can be seen in the thread
define for ipc2's task entry.

Building the application for nrf5340dk/nrf5340/cpuapp
*****************************************************

.. zephyr-app-commands::
   :zephyr-app: samples/subsys/ipc/ipc_service/static_vrings
   :board: nrf5340dk/nrf5340/cpuapp
   :goals: debug
   :west-args: --sysbuild



Open a serial terminal (minicom, putty, etc.) and connect the board with the
following settings:

- Speed: 115200
- Data: 8 bits
- Parity: None
- Stop bits: 1

Reset the board and the following message will appear on the corresponding
serial port, one is host another is remote:

.. code-block:: console

   *** Booting Zephyr OS build zephyr-v3.1.0-2383-g147aee22f273  ***
   IPC-service HOST [INST 0 - ENDP A] demo started
   IPC-service HOST [INST 0 - ENDP B] demo started
   IPC-service HOST [INST 1] demo started
   HOST [1]: 1
   HOST [1]: 3
   HOST [1]: 5
   HOST [1]: 7
   HOST [1]: 9
   ...
   <a few seconds pass>
   IPC-service HOST [INST 2] demo started
   ...
   HOST [2]: 92
   HOST [2]: 94
   HOST [2]: 96
   HOST [2]: 98
   IPC-service HOST [INST 2] demo ended.


.. code-block:: console

   *** Booting Zephyr OS build zephyr-v3.1.0-2383-g147aee22f273  ***
   IPC-service REMOTE [INST 0 - ENDP A] demo started
   IPC-service REMOTE [INST 0 - ENDP B] demo started
   IPC-service REMOTE [INST 1] demo started
   REMOTE [1]: 0
   REMOTE [1]: 2
   REMOTE [1]: 4
   REMOTE [1]: 6
   REMOTE [1]: 8
   ...
   <a few seconds pass>
   IPC-service REMOTE [INST 2] demo started
   ...
   REMOTE [2]: 95
   REMOTE [2]: 97
   REMOTE [2]: 99
   IPC-service REMOTE [INST 2] demo ended.

