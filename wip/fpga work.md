---
---

---
## PS peripherals

* Mem IO
	* DDR
	* QSPI Flash
	* eMMC
			To store device configuration
			Protocol: JEDEC
	* SD Card
	* Ethernet Phy

* Pressure gauge (RS-232)

* Fans (AXI) (undefined for now)
* Temperature sensors (AXI) (Read from Axis)
* Power sequencer (AXI)
* Front Panel LEDs (AXI) (ON or OFF from PS side, hooked up as GPIO? or via driver?)
* Momentary Button (suspend/shutdown) (interrupt from FPGA)
* Filament board (AXI) (registers R/W)
* Voltage control (AXI) (registers R/W)
* Acquisition (AXI + OCM)

* AtoD converter configuration (AXI)

* OCM RAM (Unknown)
		To pull histogram out of the FPGA every 100ms

## Unknowns challenge
* (HIGH) The AtoD converters integration with the xilinx linux device tree and kernel.
* (MEDIUM) OCM memory access
* (MEDIUM) Figuring out how to read/write over axis bus (Do we need a kernel driver for that?)
* (DEV ENV optimization)

## References
https://www.youtube.com/watch?v=9FrgIfE2xfU
https://fpga.incomeself.com/tag/xilinx-zcu106/
https://fpga.incomeself.com/tutorial-sending-an-interrupt-from-pl-to-ps-for-xilinx-zynq-ultrascale-mpsoc/#more-240

https://support.xilinx.com/s/question/0D52E00006hpgGgSAI/how-to-access-axi-registers-under-petalinux?language=en_US

https://www.xilinx.com/content/dam/xilinx/support/documents/sw_manuals/xilinx2019_1/ug1165-zynq-embedded-design-tutorial.pdf.

using axi-dma: https://www.hackster.io/whitney-knitter/introduction-to-using-axi-dma-in-embedded-linux-5264ec

xilinx petalinux repos: https://support.xilinx.com/s/article/69372?language=en_US

```
My plnx-aarch64-system.dts shows these lines:
   amba_pl@0 {
      #address-cells = <0x2>;
      #size-cells = <0x2>;
      compatible = "simple-bus";
      ranges;
      axi2regs@80002000 {
         compatible = "xlnx,axi2regs-1.1";
         reg = <0x0 0x80002000 0x0 0x1000>;
         xlnx,s00-axi-addr-width = <0xb>;
         xlnx,s00-axi-data-width = <0x20>;
      };


I had the same problem and spent a week trying to figure out whether it was a hardware or software problem. After a great deal of research i discovered the following fascinating comment in UG585…pdf:
‘Register APER_CLK_CTRL (0xF800012C)
These clocks must be enabled if you want to read from the peripheral register space.’
```



```
Ultimately your registers will appear in the memory map of the CPU. In other words, there is a specific physical address, which will access your AXI registers. If you are writing in baremetal C code, it would look like this:
volatile int *addr = (volatile int *)0x12345000;
printf("register value is %08x\n", *addr);  // read the register
*addr = 0x55;                               // write the register
Determining the physical address requires knowing:
- how the AXI registers are connected to the CPU. There are several PS-PL interfaces ("bridges") available in the Zynq. Each one has a base address.
- each register in your AXI block has a fixed address offset from the base. Typical 32-bit registers would have offsets 0x0, 0x4, 0x8, 0xc, 0x10 and so on.
The vivado/vitis tools typically will handle most of this for you, so consult with the FPGA designer.
Once you know the physical address, there are various was you can use to perform access for testing purposes:
- in u-boot the commands "md" (memory dump") and "mw" (memory write) can be used directly with the physical address. Assuming of course that the FPGA has been configured, and the bridge is active
- once Linux/Petalinux has booted, the command-line utility "devmem" or "devmem2" can be used to similarly perform read/write of physical address.
Note that Linux/Petalinux use virtual memory. So unlike the baremetal code example above, you cannot directly access a physical address. Instead it is necessary to map the physical region into the virtual address range. The "devmem" program does this, and you can also do the same in your own code.
You will find mention of UIO (userspace I/O). This provides a device ("/dev/uio0") which your application can open, and then request physical-to-virtual mapping ("mmap"). This is is very similar to what devmem does. The main reason to use UIO is to allow your application to respond to hardware interrupts. For basic register read/write, you do not need UIO.
Moving further up the complexity curve, you could write a real device driver that operates in Linux kernel space, as opposed to application (user-space). This gives more control, and more options such as using DMA for data transfer.
In the opposite direction, there are any number of 'convenience' wrappers around the basic memory-mapped I/O concept. I have no direct experience, but "Pynq" (www.pynq.io) seems to be quite popular method. And there are countless others in different languages.
```