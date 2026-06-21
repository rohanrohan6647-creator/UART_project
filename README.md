# UART_project verilog implementation
A fully synthesizable, parameterizable UART (Universal Asynchronous Receiver-Transmitter) Core implemented in verilog. Features a 16X oversampling receiver, independent baud rate generator, and modular FSM-based design.

## Overview

This project implements a complete UART communication system from scratch in Verilog, consisting of:

UART Transmitter (TX)
UART Receiver (RX)
Baud Rate Generator
Top-Level Integration Module
Loopback Verification Testbench

The design supports 8-bit serial data communication using start and stop bits and includes status signals for transmission and reception control.

## Tools 

- Xilinx Vivado 
- Verilog HDL
  
## architecture

  clk-->---|                  |                              
  rst-->---|   BAUD_RATE      |                              
           |   GENERATOR      |                              
           |                  |                              
           | tx_div = clk/baud|                              
           | rx_div = clk/(16*baud)                          
           +--------+---------+                              
                    |                                        
           +--------+--------+                                
           |                 |                                
           v (rx_enb)        v (tx_enb)                       
         +--------+--------+ +--------+--------+                
 rx-------->|              | |                |--->tx           
 rdy_clr--->| RECEIVER     | | TRANS          |--->tx_busy      
            | (RX FSM)     | | (TX FSM)       |<---tx_data[7:0] 
            |              | |                |<---tx_start     
            +------+-------+ +----------------+                
                   |                                            
                   v                                            
        rx_data[7:0]   rx_rdy                                   

## Features

FSM-based UART transmitter and reciever.
8-bit serial data transmission and reception.
Start bit detection.
Stop bit verification.
Baud rate generation from system clock.
Busy signal for transmitter status.
Data ready signal for received data.
Modular and reusable RTL design.

## Verification

The testbench performs loopback verification by connecting the transmitter output directly to the receiver input.

Verification includes:
Reset functionality testing.
Transmission of multiple data bytes.
Reception accuracy verification.
Busy signal validation.
Ready signal validation.
End-to-end UART communication testing.

## Report
src/uart_tx — UART Transmitter
src/uart_rx.v — UART Receiver
src/uart_baud_rate — Baud Rate Generator
src/uart_top — Top-Level UART Integration
tb/uart_tb — Verification Testbench
