# Part 1 - FIR Filter

## Objective

The objective of this lab is to design, implement, and test a finite impulse response (FIR) filter using FPGA technology. The goal is to understand the theory behind FIR filters, apply digital filter design techniques, and gain practical experience in hardware design and implementation. By completing this lab, students will develop skills in FPGA programming and digital signal processing (DSP).

## A Note about Collaboration

Big project is to be accomplished in groups. All work must be from your own team members.

Hints from others can be of great help, both to the hinter and the hintee.  
Thus, discussions and hints about the assignment are encouraged. However, the project must be coded and written up in groups (you may not show, nor view, any source code from other students’ groups). We may use automated tools to detect copying.

Use Emails/LMS to ask questions or come visit us (203B3) during office hours.  
We want to see you succeed, but you have to ask for help.

## Overview

In this lab, students will design an FIR filter using Verilog or SystemVerilog. The focus will be on understanding the filter design process, coding the filter architecture, and running simulations to verify the functionality of the FIR filter. Students are required to simulate the design to confirm its correctness.

For those seeking additional credit, there is an option to synthesize the design onto an FPGA and perform real-time testing. This will allow students to demonstrate their filter implementation on hardware, further reinforcing their understanding of FPGA-based digital signal processing (DSP).

The lab will include the following steps:

- Understanding the theory behind FIR filter design.
- Implementing the FIR filter architecture using HDL.
- Running simulations to verify the functionality of the filter.
- Optional: Synthesizing the design on an FPGA and conducting real-time testing for extra credit.

## Background

Finite Impulse Response (FIR) filters are an essential component in digital signal processing (DSP) systems, widely used for tasks such as noise reduction, signal smoothing, and frequency selection. FIR filters are known for their stability and linear phase properties, making them suitable for various applications that require precise signal manipulation.

In digital systems, FIR filters are typically implemented using discrete-time convolutions of the input signal with a set of filter coefficients. These coefficients determine the filter's frequency response, and they can be designed to pass, reject, or attenuate specific frequency bands. The number of coefficients, or "taps," directly impacts the filter's performance, with more taps generally leading to more accurate filtering but also increased computational complexity.

Below is an 8th-order direct form FIR filter. Generally, increasing the filter order (taps) improves the filter's performance by providing better signal filtering and more precise frequency response. However, when implementing such a design in hardware, the issue of timing becomes critical. Since each tap is implemented as a combinational element, the longer the chain, the more difficult it becomes to meet timing constraints, resulting in a lower maximum operating frequency.

![[./images/fir_diagram.png]]

To address this, pipelining techniques can be applied. By introducing pipeline stages between the taps, the combinational delay is reduced, allowing for higher clock frequencies and improved overall performance in the hardware implementation.

![[./images/fir_pipelined_diagram.png]]

The above schematic is just an example of a pipelined FIR filter. You are not required to follow this design exactly and are encouraged to propose your own design approach. Feel free to explore different architectures or optimizations that suit your specific implementation and performance goals.

## Assignment Overview

In this lab assignment, you will design and simulate an FIR filter using Verilog or VHDL. Your task is to implement the FIR filter based on your specifications and verify its functionality through simulation. To assist you in this process (though you are welcome to use your own resources if preferred), the following resources are provided:

- A **testbench** to simulate and verify the FIR filter design.
- **Three input signal samples** to be used for testing the filter’s performance.

Your primary goal is to complete the FIR filter design and verify its operation through simulation using the provided testbench and input signals. For extra credit, you can synthesize the design and demo it on an FPGA for real-time testing.

## Samples

We provide you with three sample signals with a testbench to help you get started with your FIR filter design. The goal is for your design to effectively filter out the noisy components from each signal. You are encouraged to use MATLAB or Python to analyze the frequency components of these signals and determine which frequencies need to be filtered out. Additionally, you can use the "Filter Designer" application in MATLAB to assist in generating the appropriate filter coefficients.

The sample signals are 24-bit and located in `samples` folder. The input and expected filtered signals are shown below. I believe you can achieve better results with your design and improvements. The provided sample signals include:

1. **Noisy sine waves** (`sine.hex`): A set of sine waves with added noise. Your filter should clean up the signal by removing the unwanted noise while preserving the sine wave.   ![[./images/sine_wave.png]]
   
2. **Audio sample with high-pitched hissing noise** (`audio.wav, audio.hex`): This audio is taken from the video "[The Lost 1984 Video: young Steve Jobs introduces the Macintosh](https://youtu.be/2B-XwPjn9YY)" and has a sample rate of 44.1 kHz, with a duration of 15 seconds. The audio that contains a high-frequency hissing sound. Your filter should target and remove this high-frequency noise while keeping the Steve Jobs's voice intact.
   Two Python scripts are provided in the `utils` folder to help you convert between `.wav` and `.hex` files. It's recommended that you review the scripts to understand how they work and make any necessary tweaks to suit your needs. Please note, I am not responsible if they don't work as expected.  ![[./images/audio_wave.png]]
   
3. **Noisy ECG signal** (`ecg.hex`): A typical ECG (electrocardiogram) signal with noise. The goal is to filter out the noise and recover the clean ECG waveform for accurate analysis.   ![[./images/ecg_wave.png]]

Use these signals to test your FIR filter design, ensuring it successfully removes the noisy components without distorting the essential parts of the signal.

## For Credit

- **1 point**: Demonstrates a basic understanding of FIR filters and designs the specifications for the FIR filter.
- **2 points**: Completes the RTL design for the FIR filter, ensuring it aligns with the given specifications. These points are awarded only if you successfully simulate and verify the filter's functionality with at least one sample.
- **3 points**: Successfully simulates the FIR filter design with the provided input samples. Your analysis should explain how well the filter performs, identifying any issues in filtering and frequency response.
- **2 points**: Implements a pipelined/parallelized architecture to achieve higher operating frequency.
- **2 points**: Synthesizes the design and performs a live demo on an FPGA, demonstrating real-time performance and signal processing.
- Bonus points:
	- Fully parameterizable FIR filter 
	- Demonstrates the FIR filter's performance using real-world signals (audio signal)
	- Adaptive FIR filter with dynamically updated coefficients based on signal input
	- You can propose your own idea
	- If your filter results are not optimal, you should analyze and explain why the result is insufficient, and propose a solution to improve it. Even if the filter performance is not ideal, a well-explained analysis can still earn bonus points.

## Reporting Requirements

Your report should be concise but detailed enough to clearly explain your design process, simulations, and results. Make sure to:
- Include explanations of the design choices you made, particularly if you implemented a pipelined architecture or any optimizations.
- Show clear evidence of how your FIR filter performs with the provided input signals, including graphs or waveforms and analysis.
- If the filter doesn’t perform well, offer a detailed analysis of why the results are not as expected and propose improvements or solutions.
  
Your report should focus on quality rather than length. While it shouldn’t be excessively long, it needs to be thorough and well-structured. Points will be deducted for poor reporting, such as missing key details, insufficient analysis, or unclear presentation. Make sure to present your work in a professional and readable format.

## How To Turn In Your Solution

This semester we will be using LMS, simply submit the zip file with your reports and codes.

## Demos and Late Penalty

We will have demo / presentation times on of class times on or near the due date. Since we will demo from the files in your zip, it is possible that you’ll demo on a following day.

**Define Late:** Lateness is determined by the file dates of your submission on LMS.