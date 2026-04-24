# Laboratory-Tusk

### Laboratory #5 (Experiment 1) :page_facing_up: 

### Explanation of Experiment:
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The experiment is a comprehensive look at the end-to-end communication process of a QPSK system using the Emona Telecoms-Trainer 101. It begins with Serial-to-Parallel (S/P) conversion, where a fast bitstream is split into two slower streams (even and odd bits). These streams modulate two separate carriers that are 90 degrees apart (orthogonal), which are then summed to create the QPSK signal. The demodulation process involves using product detectors to separate the "I" and "Q" components, low-pass filtering to remove high-frequency artifacts ($2f_c$), and comparators to restore sharp logic levels. The lab also tests the system's robustness by introducing noise and phase errors to observe how they impact data integrity.
</p>

---

<details>
<summary>EXPERIMENT 1 - Full Demodulation of a QPSK Signal</summary> 

**INTRODUCTION**
* Amplitude Shift Keying, often referred to as On-Off Keying (OOK), is a basic digital modulation technique where the binary bitstream controls the carrier amplitude. In this scheme, the carrier is transmitted at full power for a logic high and is completely suppressed for a logic low. This experiment focuses on creating the ASK envelope and using an envelope detector to strip the carrier away for data recovery.

**EXPLANATION**

The experiment is structured to demonstrate the full lifecycle of a digital signal within a QPSK system:

* Bit Stream Manipulation: The process begins with a high-speed serial data stream that is converted into two slower parallel streams (In-phase and Quadrature) using a Serial-to-Parallel (S/P) converter.

* Signal Generation: These parallel streams modulate two orthogonal carriers through multipliers, which are then summed to create a single QPSK waveform.

* Demodulation and Recovery: The receiver uses product detectors (multipliers) to separate the I and Q components, followed by Low Pass Filters to extract the baseband data and comparators to restore sharp logic levels.

* Performance Analysis: The experiment concludes by testing the system's sensitivity to channel noise and phase synchronization errors to observe how these factors lead to bit errors and data corruption.

<details><summary><b>[View EXPERIMENT 1 - Full Demodulation of a QPSK Signal Details]</b></summary><br>https://github.com/EmmanAbad/Laboratory-Tusk/blob/main/EXPERIMENT%201%20-%20Full%20Demodulation%20of%20a%20QPSK%20Signal.md<br></details>

</details>

---

### Learnings: 
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;This lab demonstrated that QPSK is highly efficient but inherently fragile. Seeing the actual "phase jumps" on an oscilloscope made the mathematical theory intuitive. I learned that the S/P conversion is the "heartbeat" of the system, slowing down data so the carrier can handle it efficiently. Furthermore, the phase error analysis was a major highlight, proving that even a small shift in synchronization can cause channels to "leak" into one another, resulting in total crosstalk or inverted logic.
</p>

---

### Conclusion:
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The experiment successfully validated the principles of QPSK modulation and demodulation. By following a systematic approach, the setup confirmed that two independent bitstreams can be carried on a single frequency without interference, provided the carriers remain orthogonal. While the system demonstrated high data throughput, the tests with noise and phase offsets highlighted the necessity of a precise phase reference at the receiver. Ultimately, the experiment proved that as long as timing and phase are strictly controlled, the original information can be recovered with high fidelity.
</p>
