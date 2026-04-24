# EXPERIMENT 1 - Full Demodulation of a QPSK Signal :page_facing_up: 
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;At its core, QPSK is basically two BPSK signals running on the same frequency but shifted in phase so they don't interfere with each other. While BPSK is essentially a DSBSC scheme using digital data for the message, QPSK sends two bits at a time. It's a bit of a trick, though; because we convert a fast serial bitstream into two slower parallel ones, the actual symbol rate stays the same while the data throughput doubles.

&nbsp;&nbsp;&nbsp;&nbsp;The main reason we bother with this complexity is spectral efficiency. By sending two bits per symbol, we only need half the RF spectrum that BPSK would require for the same bit rate. However, this comes with a catch. The receiver has to be much smarter. It needs to perfectly separate these "I" and "Q" components using product detectors and then put them back in the right order using a parallel-to-serial converter. If the local carrier at the receiver isn't perfectly aligned with the transmitter, the two channels "leak" into each other, which leads to total data corruption.
</p>

<img width="422" height="296" alt="image" src="https://github.com/user-attachments/assets/0e8c9d9d-067c-4bf1-b7db-8013ef689332" />

<img width="432" height="259" alt="image" src="https://github.com/user-attachments/assets/f8f531a2-5d6d-4c9d-b258-bf4545098cc3" />

---

### Introduction 
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;Quadrature Phase Shift Keying (QPSK) represents a major step up from basic binary modulation. In modern telecommunications, efficiency is everything, and QPSK allows us to transmit double the amount of data compared to BPSK without needing more bandwidth. This is achieved by using two carriers that are mathematically orthogonal—meaning they are 90 degrees apart—to carry two separate bitstreams (the In-phase and Quadrature components) at the same time. This lab explores the practical implementation of this theory, from the initial bit-splitting to the final reconstruction of the original serial data.
</p>

---

### Objectives
* To understand the hardware implementation of serial-to-parallel (S/P) and parallel-to-serial (P/S) converters.
* To model the mathematical generation of a QPSK signal using orthogonal carriers.
* To demonstrate the demodulation process using product detection and low-pass filtering.
* To analyze how channel noise and carrier phase errors affect the integrity of the recovered digital data.

---

### Equipment
* Emona Telecoms-Trainer 101 (and power-pack)
* Emona ETT-101-20 QPSK DEMOD expansion board
* Dual-channel 20MHz oscilloscope
* Three Emona lead sets
* Assorted patch leads

---

**Procedure – Part A: Verifying S/P and P/S Conversion**
1. Ensure the ETT-101 is powered off before plugging in the QPSK DEMOD board.
2. Set the Oscilloscope timebase to 0.5ms/div and both channels to 2V/div with DC coupling.
3. Connect the Bit Clock from the Sequence Generator to the 'CLK' input of the 2-bit S/P converter.
4. Patch the 'DATA' output of the Sequence Generator to the 'IN' socket of the S/P converter.
5. Connect the 'X1' and 'X2' parallel outputs of the S/P converter to the corresponding 'X1' and 'X2' inputs on the 2-bit P/S converter.
6. Trigger the oscilloscope using the 'SYNC' output of the Sequence Generator to ensure a stable display.
7. Observe the original serial data on Channel 1 and the reconstructed P/S output on Channel 2 to verify the bit sequence.

<img width="494" height="242" alt="image" src="https://github.com/user-attachments/assets/43784367-0d7a-4af7-999d-9fee20376a32" />

<img width="422" height="209" alt="image" src="https://github.com/user-attachments/assets/664d8225-8f8f-4e48-bd43-7732f7c1fc76" />

<img width="422" height="209" alt="image" src="https://github.com/user-attachments/assets/3241da0c-4587-42dd-8eab-3e6c0f35fb48" />

---

**Procedure – Part B: Setting up the Zero-Crossing Detector**
1. Connect a 100kHz sine wave to the 'carrier' input of the Phase Shifter module.
2. Use the Phase Shifter to create a $90^\circ$ difference between the original 100kHz carrier (I-channel) and the shifted version (Q-channel).
3. Patch the 'Even bits' from the S/P converter into the DC input of Multiplier 1.
4. Patch the 'Odd bits' from the S/P converter into the DC input of Multiplier 2.
5. Connect the I-carrier to Multiplier 1 and the Q-carrier to Multiplier 2 to generate two independent BPSK signals.
6. Sum the outputs of both multipliers using the Adder module to synthesize the final QPSK waveform.
7. Monitor the Adder output on the scope and observe the phase shifts occurring at symbol boundaries.

<img width="414" height="347" alt="image" src="https://github.com/user-attachments/assets/698ca0de-8443-440e-98fb-91cd3889e750" />

<img width="491" height="321" alt="image" src="https://github.com/user-attachments/assets/87cf6134-9559-4eb4-aa93-d9e41b754939" />

---

**Procedure – Part C: Demodulating QPSK using the ETT-101-20 Board**
1. Connect the output of the QPSK generator (from Part B) to the 'IN' socket of the QPSK DEMOD board.
2. Provide the 100kHz local carrier to the board’s carrier input to enable product detection.
3. Patch the internal 'I' and 'Q' outputs of the demodulator to the dual-trace oscilloscope.
4. Observe the "fuzzy" signal appearing at the multiplier outputs before any filtering is applied.
5. Pass these raw outputs through the on-board Low Pass Filters (LPF) to recover the baseband DC levels.
6. Connect the filtered signals to the on-board Comparators to restore the sharp logic levels of the bits.
7. Verify that the recovered even and odd bitstreams match the original parallel bits at the transmitter.

<img width="449" height="221" alt="image" src="https://github.com/user-attachments/assets/1fb5cf17-a7cb-4fc8-8ce9-fb4a9ac0789a" />

---

**Procedure – Part D: Effects of Noise on the QPSK Link**
1. Insert the Noise Generator module into the circuit between the transmitter and the receiver.
2. Use an Adder to combine the clean QPSK signal with the noise output.
3. Set the Noise Generator to its minimum setting and observe the recovered data on the scope.
4. Slowly increase the noise amplitude while watching the 'DATA' output of the P/S converter.
5. Identify the point where the noise causes the comparator to "flicker," indicating the onset of bit errors.
6. Adjust the gain of the Master Signals to see if a stronger carrier improves the signal-to-noise ratio (SNR).
7. Document the visual distortion of the QPSK carrier on the oscilloscope as noise is added.

<img width="368" height="343" alt="image" src="https://github.com/user-attachments/assets/6b17d213-eab4-4329-b5a7-3ec589098f42" />

<img width="476" height="323" alt="image" src="https://github.com/user-attachments/assets/e074ff38-3c24-4d33-b1c5-639a4604652e" />

<img width="461" height="262" alt="image" src="https://github.com/user-attachments/assets/73e084b1-37ac-4173-a814-7e71fc0977c1" />

---

**Procedure – Part E: Investigating Carrier Phase Errors**
1. Return the system to a clean state without noise and ensure the data is being recovered correctly.
2. Locate the Phase Shifter being used for the local carrier at the receiver.
3. Slowly rotate the phase control knob to introduce a small phase error.
4. Observe the recovered data and note the point where the bit sequence becomes unstable.
5. Set the phase shift to exactly $90^\circ$ and observe how the I and Q channels effectively "swap" data.
6. Increase the phase shift to $180^\circ$ and verify that the output bits are logically inverted (1 becomes 0).
7. Return the phase to $0^\circ$ and confirm that the receiver re-synchronizes with the original data stream.

**Procedural Learning**
###### The Foundation of Timing and Synchronization
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The initial stage of the procedure focused on the transformation of data through **Serial-to-Parallel (S/P)** and **Parallel-to-Serial (P/S)** conversion. This phase illustrated that data reconstruction is fundamentally tied to a shared timing reference. By patching the Bit Clock across both ends of the system, it became clear that without a synchronized clock, the receiver is unable to delineate individual bit boundaries, rendering the data unrecoverable. This stage also highlighted the inherent latency in symbol-based systems; the hardware must "buffer" incoming bits to form a symbol, creating a visible time offset between the input and the final reconstructed serial output.
</p>

###### Orthogonality and Signal Generation
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;As the procedure moved into signal generation, the physical requirement for **orthogonality** was demonstrated. Modeling a QPSK generator using individual multipliers and a phase shifter proved that the $90^\circ$ relationship between the In-phase (I) and Quadrature (Q) carriers is a mechanical necessity rather than just a mathematical convenience. Observing the summation of these two BPSK signals through an Adder module revealed that the final QPSK waveform is a vector sum, where phase transitions represent the encoded bit-pairs. This practical step provided a tangible look at how a single carrier can be manipulated to carry twice the information density of a standard binary system.
</p>

###### Demodulation and Baseband Recovery
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The demodulation and recovery procedures further clarified the necessity of multi-stage signal processing. The use of product detectors confirmed that while multiplication successfully shifts the signal back to baseband, it simultaneously introduces high-frequency artifacts ($2f_c$) that obscure the data. The subsequent procedural requirement to utilize **Low Pass Filters (LPF)** demonstrated their role as essential "cleaning" components, stripping away these artifacts to reveal stable DC levels. Finally, the use of comparators illustrated the decision-making process in digital systems, showing how a noisy analog level is "squared up" into a crisp logic state based on specific voltage thresholds.
</p>

###### Robustness and Phase Sensitivity
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The most significant procedural takeaway occurred during the analysis of carrier phase errors and noise. Intentionally introducing a phase shift in the local carrier proved just how fragile QPSK can be. A small alignment error led to immediate **cross-talk**, where the I and Q channels began to "bleed" into one another, while a $180^\circ$ shift resulted in total logic inversion. These steps reinforced the idea that high spectral efficiency comes at the cost of increased receiver complexity and a strict requirement for phase synchronization.
</p>

---

### Questions and Answers 
**Question 1: Are the two data signals the same? Explain your answer.**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;Yes, they represent the same binary sequence. If the input is $1011$, the output will eventually show $1011$. However, they are not identical in real-time because the reconstruction process creates a small delay.
</p>

**Question 2: Why are the two signals offset in this way?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The offset is a result of the propagation delay through the converters. The S/P converter has to "collect" two bits before it can output a symbol, and the P/S converter has to wait for those bits to be ready before shifting them back out. This buffering time causes the output to lag behind the input.
</p>

**Question 3: Are the $PSK_I$ and $PSK_Q$ signals and the QPSK signal related?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;They are fundamentally linked. The QPSK signal is the vector sum of the I and Q signals. Because the carriers are $90^\circ$ apart, they don't cancel each other out; instead, they combine to form a wave with four possible phase states.
</p>

**Question 4: Looking at the QPSK signal on the scope, can you see the phase change?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;Yes. Whenever the digital bit-pair changes from one state (e.g., $00$) to another (e.g., $11$), the sine wave shows a sharp discontinuity or a "jump" in its cycle, which marks the phase transition.
</p>

**Question 5: Describe the two signals on the outputs of the two Multiplier modules.**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The outputs are a mixture of low-frequency data and high-frequency noise. Specifically, you see the baseband bitstream "riding" on top of a signal that is double the carrier frequency ($2f_c$), which makes the waveform look thick and distorted.
</p>

**Question 6: Why are the Low Pass Filters necessary for the demodulation?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The multipliers produce an unwanted $2f_c$ component. The LPF acts as a "cleanup" tool, blocking those high frequencies and allowing only the original DC bit levels to pass through to the next stage.
</p>

**Question 7: Describe the effect that adding noise has on the QPSK signal.**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;Noise makes the carrier appear "fuzzy" or blurred. On an oscilloscope, the clean lines of the sine wave widen, effectively masking the precise phase of the signal.
</p>

**Question 8: What is the effect of the noise on the recovered digital data?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;It causes bit errors. If the noise is strong enough to push the signal across the comparator’s threshold at the wrong time, the receiver will output the wrong bit, leading to data corruption.
</p>

**Question 9: What happened to the recovered digital data (90° shift)?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The data is lost or scrambled. A $90^\circ$ error causes the I-branch to receive the Q-branch's data and vice-versa, which is essentially total crosstalk.
</p>

**Question 10: What happened to the recovered digital data (180° shift)?**
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The recovered bits become inverted. Every '1' is interpreted as a '0' and every '0' as a '1' because the receiver’s reference is exactly the opposite of the transmitter's.
</p>

---

### Learnings
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;This laboratory session provided a very clear look at how complex modulation actually works on the bench. It’s one thing to see the math on a whiteboard, but seeing the actual phase "jumps" on the scope makes it much more intuitive. I learned that the serial-to-parallel conversion is essentially the heartbeat of the system—it's what allows us to slow down the data so the carrier can handle it more efficiently. Additionally, the phase error section was a real eye-opener; it shows just how fragile QPSK can be if the transmitter and receiver aren't perfectly in sync. Even a small shift can flip the logic or mix up the channels entirely.
</p>

---

### Conclusion
<p align="justify">
&nbsp;&nbsp;&nbsp;&nbsp;The experiment successfully demonstrated the principles of FM demodulation using the Emona Telecoms-Trainer 101. By following the systematic procedures from Part A to E, I was able to observe how a frequency-modulated carrier is progressively transformed back into its original message form. The zero-crossing detector proved to be an effective demodulator, capable of handling various signal types with high fidelity. In conclusion, the setup confirmed that as long as the pulse width is shorter than the period of the highest frequency in the FM signal, the original information can be accurately recovered through duty cycle variations and low-pass filtering.
</p>
