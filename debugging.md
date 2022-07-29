How would you go about locating the cause of a stack overflow or watchdog timer reset?

Stack Overflow:
- One of the ways to detect a stack overflow is to store the address of the top of the stack in a static variable, recursively call a function and capture the current stack pointer at every call and 	calculate the difference between the 2 addresses. The closer your difference is to 0, the closer you are to a stack overflolw.
- Adjust the size of the stack based on your tolerance.
- I implemented a data transfer of (96 * 1024) bytes as a part of the raw readings transfer between our 2 subsystems, while this may be obvious, do not store this array as a local array, even if you have stack space. Declare it as a static and retain it in the global data space.
- Single-step debugging may help in determining at what line of code the firmware crashes, but "stopping and continuing" code might be quite difficult in an embedded environment, especially with an RTOS.
- 1 break point per rerun cycle can help you determine the code line and the call stack can help you check to see the function calls that either have recursion or a large number of variables or arrays.
- Especially in BLE implementation, one of the overlooked mistakes while adding a BLE device, central or peripheral, is not adjusting the size of the BLE stack.
- The SDK of the ble stack provider also has functions to capture this and inform us about the size requirements. 

Watchdog Timer reset:
- Quite a few chip vendors will have a reset reason register that can be read that informs us if a watchdog reset has occured. 
- Read the register at boot-up and single-step/print out/store in persistent storage for future debugging.
- I have used the Nordic RESETREAS register to do the same.
- If a reset reason register is not present, store the reason in persistent storage during the watchdog interrupt and read it back on bootup. 
- Keep in mind, we have very few clock cycles inside an interrupt. Storing the PC will help us pin point the line of code.
