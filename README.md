# powerseq-FPGA-IP
A power sequencer VHDL code project for digital board designs with glue logic FPGA
Original release here on GitHub in 2024

To download: Click the zip file, on the next page click "view raw" to download it.

A less restrictive license called "BSD zero clause" is used. This will allow companies to use it in their product without restrictions or obligations.
The BSD 0-clause license: Copyright (C) 2024 by Istvan Nagy buenoshun@gmail.com 
Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted. THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE.

A power sequencer is used in large complex digital circuit board (PCB) designs, like computer motherboards, router line cards or telecom boards. These boards have many voltage regulators (rails) that have to be turned on one by one in a sequence. This sequencer does that job. It typically starts a sequence when a power master device like a management controller (BMC or IPMC) asserts a main power on signal. If we don't have a management controller on the PCB, then the enable can be tied logic high, so the board will power up when the input power is applied, through a power cord or by plugging the board into a chassis.
This sequencer also supports power failure mitigation by emergency shutdown, debug mode (with emergency shutdown disabled), capturing failed rails in a large vector made available on the ports. The internal execution only happens every several thousand clock cycles, so it is not happening at the MHz rate. This rate is adjustable for debug purposes by changing the length of the tick timer. It stays off until input power cycle.

The main sequencer code is: powerseq_mod.vhd
This is a 128-rail power sequencer.
The user is supposed to instantiate it into a glue logic FPGA code, used for motherboard power management. After instantiation the user has to assign named power rail enable and PowerGood signals to the numbered rails. The module provides a rail enable and a PowerGood vector, each bit is for a different rail.
We can use the file pseq_3redundant.vhd to make the sequencer SEU-immune, between the module and the top level user code.
Two example VHDL files are provided about how to use the sequencer module: example1.vhd and example2.vhd. These can be used as templates, but have to be completely rewritten for every new board design.
An instantiation template and a simulation test bench is provided. 

