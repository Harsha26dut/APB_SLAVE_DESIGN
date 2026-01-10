import React from 'react';

const APBSlavePackage = () => {
  return (
    <div className="p-6 bg-slate-50 min-h-screen font-sans text-slate-800">
      <div className="max-w-4xl mx-auto space-y-8">
        <header className="border-b pb-4">
          <h1 className="text-3xl font-bold text-slate-900">APB Slave IP Design Package</h1>
          <p className="text-slate-600 mt-2">Complete RTL, Verification, and Backend Scripts</p>
        </header>

        <section className="space-y-4">
          <h2 className="text-xl font-semibold border-l-4 border-blue-500 pl-3">1. RTL Design (`rtl/apb_slave.sv`)</h2>
          <div className="bg-slate-900 text-slate-300 p-4 rounded-lg overflow-x-auto text-sm shadow-inner">
            <pre>{`module apb_slave #(
    parameter ADDR_WIDTH = 32,
    parameter DATA_WIDTH = 32
)(
    input  logic                   pclk,
    input  logic                   presetn,
    input  logic [ADDR_WIDTH-1:0] paddr,
    input  logic                   psel,
    input  logic                   penable,
    input  logic                   pwrite,
    input  logic [DATA_WIDTH-1:0] pwdata,
    output logic [DATA_WIDTH-1:0] prdata,
    output logic                   pready,
    output logic                   pslverr
);

    // Internal Register Bank (Memory)
    logic [DATA_WIDTH-1:0] mem [0:63]; 

    // State definitions
    typedef enum logic [1:0] {
        IDLE   = 2'b00,
        SETUP  = 2'b01,
        ACCESS = 2'b10
    } apb_state_t;

    apb_state_t current_state, next_state;

    // FSM State Transition
    always_ff @(posedge pclk or negedge presetn) begin
        if (!presetn)
            current_state <= IDLE;
        else
            current_state <= next_state;
    end

    // FSM Logic
    always_comb begin
        next_state = current_state;
        pready     = 1'b0;
        pslverr    = 1'b0; // Default: No error

        case (current_state)
            IDLE: begin
                if (psel && !penable)
                    next_state = SETUP;
            end
            
            SETUP: begin
                if (psel && penable)
                    next_state = ACCESS;
                else if (!psel)
                    next_state = IDLE;
            end

            ACCESS: begin
                pready = 1'b1;
                if (psel && !penable)
                    next_state = SETUP;
                else
                    next_state = IDLE;
            end
        endcase
    end

    // Data Transfer Logic
    always_ff @(posedge pclk) begin
        if (psel && penable && pready) begin
            if (pwrite)
                mem[paddr[5:0]] <= pwdata;
            else
                prdata <= mem[paddr[5:0]];
        end
    end

endmodule`}</pre>
          </div>
        </section>

        <section className="space-y-4">
          <h2 className="text-xl font-semibold border-l-4 border-green-500 pl-3">2. Synthesis Script (`scripts/synth.tcl`)</h2>
          <div className="bg-slate-900 text-slate-300 p-4 rounded-lg overflow-x-auto text-sm shadow-inner">
            <pre>{`# Yosys Synthesis Script for APB Slave
read_liberty -lib lib/NangateOpenCellLibrary_typical.lib
read_verilog -sv rtl/apb_slave.sv

# Check hierarchy
hierarchy -top apb_slave

# High-level synthesis
proc; opt; fsm; opt; memory; opt

# Mapping to internal cells
techmap; opt

# Mapping to gate library
dfflibmap -liberty lib/NangateOpenCellLibrary_typical.lib
abc -liberty lib/NangateOpenCellLibrary_typical.lib

# Cleanup
clean

# Output results
write_verilog reports/netlist.v
stat -liberty lib/NangateOpenCellLibrary_typical.lib`}</pre>
          </div>
        </section>

        <section className="space-y-4">
          <h2 className="text-xl font-semibold border-l-4 border-orange-500 pl-3">3. Timing Constraints (`constraints/top.sdc`)</h2>
          <div className="bg-slate-900 text-slate-300 p-4 rounded-lg overflow-x-auto text-sm shadow-inner">
            <pre>{`# 50 MHz Clock Period (20ns)
create_clock -name pclk -period 20 [get_ports pclk]

# Define Input/Output Delays
set_input_delay -clock pclk 2.0 [get_ports {paddr penable psel pwrite pwdata presetn}]
set_output_delay -clock pclk 2.0 [get_ports {prdata pready pslverr}]

# Design Load
set_load 0.005 [all_outputs]`}</pre>
          </div>
        </section>

        <footer className="pt-8 text-center text-xs text-slate-400">
          Built for Harsha's APB Slave Design Portfolio
        </footer>
      </div>
    </div>
  );
};

export default APBSlavePackage;`
