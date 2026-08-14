# 8 × 8 RAM Using Verilog HDL

## Overview

RAM stands for **Random Access Memory**. It is a type of memory that allows data to be written to and read from different memory locations.

In this project, an **8 × 8 RAM** is designed and simulated using Verilog HDL.

The RAM contains:

* 8 memory locations
* 8-bit data at each location
* 3-bit address
* Write enable control
* Clock signal
* Data input
* Data output

## Features

* 8 memory locations
* 8-bit data width
* 3-bit address
* Synchronous write operation
* Synchronous read operation
* Write enable control
* Verilog HDL implementation
* Testbench included
* VCD waveform generation
* Icarus Verilog and GTKWave compatible

## RAM Size

```text
Number of locations = 8
Data width           = 8 bits
Address width        = 3 bits
```

Therefore:

```text
RAM Size = 8 × 8 bits
         = 64 bits
```

## Block Diagram

```text
                  ┌─────────────────────┐
                  │                     │
 address[2:0] ───►│                     │
                  │                     │
 data_in[7:0] ──►│      8 × 8 RAM      │───► data_out[7:0]
                  │                     │
 clk ────────────►│                     │
                  │                     │
 we ─────────────►│                     │
                  │                     │
                  └─────────────────────┘
```

## Inputs and Outputs

| Signal     | Direction |  Width | Description             |
| ---------- | --------- | -----: | ----------------------- |
| `clk`      | Input     |  1 bit | Clock signal            |
| `we`       | Input     |  1 bit | Write enable            |
| `address`  | Input     | 3 bits | Selects memory location |
| `data_in`  | Input     | 8 bits | Data to be written      |
| `data_out` | Output    | 8 bits | Data read from memory   |

## Memory Organization

The RAM has 8 locations:

```text
Address 000 → Memory location 0
Address 001 → Memory location 1
Address 010 → Memory location 2
Address 011 → Memory location 3
Address 100 → Memory location 4
Address 101 → Memory location 5
Address 110 → Memory location 6
Address 111 → Memory location 7
```

## Project Structure

```text
ram-verilog/
│
├── README.md
│
├── rtl/
│   └── ram.v
│
├── testbench/
│   └── ram_tb.v
│
└── simulation/
    └── waveform.png
```

## Verilog Design

The main design file is:

```text
rtl/ram.v
```

```verilog
module ram (
    input  wire       clk,
    input  wire       we,
    input  wire [2:0] address,
    input  wire [7:0] data_in,
    output reg  [7:0] data_out
);

    reg [7:0] memory [0:7];

    always @(posedge clk) begin
        if (we)
            memory[address] <= data_in;

        data_out <= memory[address];
    end

endmodule
```

## Working Principle

The RAM performs operations based on the `we` signal.

### Write Operation

When:

```text
we = 1
```

data is written into the selected memory location on the positive edge of the clock.

For example:

```text
Address = 000
Data In = AA
WE      = 1
```

The RAM stores:

```text
Memory[000] = AA
```

### Read Operation

When:

```text
we = 0
```

the data stored at the selected address is read.

For example:

```text
Address = 000
WE      = 0
```

The output becomes:

```text
Data Out = AA
```

## Testbench

The testbench is located at:

```text
testbench/ram_tb.v
```

The testbench performs the following operations:

1. Initializes the RAM signals.
2. Writes `AA` to address `000`.
3. Writes `55` to address `001`.
4. Writes `F0` to address `010`.
5. Writes `0F` to address `011`.
6. Writes `A5` to address `100`.
7. Disables writing.
8. Reads each previously written address.
9. Displays the results.
10. Generates a VCD waveform file.

## Test Data

| Operation | Address | Data |
| --------- | :-----: | :--: |
| Write     |   000   |  AA  |
| Write     |   001   |  55  |
| Write     |   010   |  F0  |
| Write     |   011   |  0F  |
| Write     |   100   |  A5  |
| Read      |   000   |  AA  |
| Read      |   001   |  55  |
| Read      |   010   |  F0  |
| Read      |   011   |  0F  |
| Read      |   100   |  A5  |

## Expected Simulation

During the write phase:

```text
WE = 1

Address 000 → Data In AA
Address 001 → Data In 55
Address 010 → Data In F0
Address 011 → Data In 0F
Address 100 → Data In A5
```

During the read phase:

```text
WE = 0

Address 000 → Data Out AA
Address 001 → Data Out 55
Address 010 → Data Out F0
Address 011 → Data Out 0F
Address 100 → Data Out A5
```

## Simulation Using Icarus Verilog

### Compile

```bash
iverilog -o ram_sim rtl/ram.v testbench/ram_tb.v
```

### Run

```bash
vvp ram_sim
```

The simulation generates:

```text
ram.vcd
```

## Viewing the Waveform

Open the generated VCD file using GTKWave:

```bash
gtkwave ram.vcd
```

Add the following signals:

```text
clk
we
address
data_in
data_out
```

The waveform demonstrates both write and read operations.

Save the waveform screenshot as:

```text
simulation/waveform.png
```

## Applications of RAM

RAM is widely used in:

* Computer systems
* Microcontrollers
* Microprocessors
* FPGA designs
* Digital signal processing
* Data buffering
* Cache memory
* Temporary data storage

## Advantages

* Fast data access
* Data can be both read and written
* Any memory location can be accessed using its address
* Useful for temporary data storage

## Limitations

* RAM is generally volatile memory.
* Stored data may be lost when power is removed.
* More hardware is required compared with simple registers.

## RAM vs ROM

| Feature           | RAM               | ROM                           |
| ----------------- | ----------------- | ----------------------------- |
| Read              | Yes               | Yes                           |
| Write             | Yes               | No                            |
| Data modification | Possible          | Normally not during operation |
| Typical use       | Temporary storage | Fixed data/program storage    |
| Volatile          | Usually           | Usually non-volatile          |

## Conclusion

An 8 × 8 RAM was successfully designed using Verilog HDL.

The design supports both write and read operations. A Verilog testbench was developed to verify the functionality by writing different values into memory locations and reading them back.

The simulation waveform can be viewed using GTKWave.

## Tools Used

* Verilog HDL
* Icarus Verilog
* GTKWave
* GitHub

## Author

Digital Design / Verilog HDL Project

## License

This project is intended for educational purposes.
