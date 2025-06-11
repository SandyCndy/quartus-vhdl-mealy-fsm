# quartus-vhdl-mealy-fsm

```markdown
# 🔁 Mealy FSM Sequence Detector (Detects "11011")

This project implements a **Mealy-type Finite State Machine (FSM)** in **VHDL** using **Intel Quartus Prime**, designed to detect the binary sequence **11011**.

## 📂 Project Files

- `melay_sandy.vhd` — VHDL source code for the Mealy FSM
- Simulation waveform (ModelSim)
- RTL Viewer and State Machine Viewer screenshots

---

## ⚙️ What is an FSM?

A **Finite State Machine (FSM)** is a digital model that transitions between a **finite number of states** based on inputs and produces outputs accordingly.

---

## 🔑 Key Features of Mealy Machine

- Output depends on **both state and input**
- **Faster output response**
- **Fewer states** compared to Moore machine
- Output can change **without state transition**
- Compact and efficient design
- Ideal for **sequence detection**

---

## 🧠 FSM Design Overview

### ➕ Sequence to Detect: `11011`

### 📌 States Used:
- `A` – Initial state
- `B` – First `1` detected
- `C` – `11` detected
- `D` – `110` detected
- `E` – `1101` detected → Next input `1` triggers output `1`

### 🖼️ State Transition Summary:
```

A --1--> B --1--> C --0--> D --1--> E --1--> A (Output = 1)
\                        /
\-------- else --------
![WhatsApp Image 2025-06-11 at 11 38 09_abd77ddb](https://github.com/user-attachments/assets/90654b74-cbe2-4360-b007-b43a10a51095)
````

---

## 💾 VHDL Code (`melay_sandy.vhd`)

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity melay_sandy is
   port (
      clk   : in  STD_LOGIC;
      rst   : in  STD_LOGIC;
      d_in  : in  STD_LOGIC;
      d_out : out STD_LOGIC
   );
end melay_sandy;

architecture behavioral of melay_sandy is
   type state_type is (A, B, C, D, E);
   signal state : state_type := A;
begin 
   process(clk)
   begin
      if rising_edge(clk) then
         if rst = '1' then
            state <= A;
            d_out <= '0';
         else
            case state is
               when A => 
                  if d_in = '1' then
                     state <= B;
                     d_out <= '0';
                  else
                     state <= A;
                     d_out <= '0';
                  end if;

               when B => 
                  if d_in = '1' then
                     state <= C;
                     d_out <= '0';
                  else
                     state <= A;
                     d_out <= '0';
                  end if;

               when C => 
                  if d_in = '0' then
                     state <= D;
                     d_out <= '0';
                  else
                     state <= C;
                     d_out <= '0';
                  end if;

               when D => 
                  if d_in = '1' then
                     state <= E;
                     d_out <= '0';
                  else
                     state <= A;
                     d_out <= '0';
                  end if;

               when E => 
                  if d_in = '1' then
                     state <= A;
                     d_out <= '1';
                  else
                     state <= A;
                     d_out <= '0';
                  end if;
            end case;
         end if;
      end if;
   end process;
end behavioral;
````
![WhatsApp Image 2025-06-11 at 11 37 58_b810c20f](https://github.com/user-attachments/assets/7aacc4a6-65c0-4bc3-bd00-5d149d38c279)

---

## 📊 Simulation Waveform

* Verified using **ModelSim**
* Sequence `11011` correctly produces `d_out = '1'` at the final input
* Output is asserted during state E when `d_in = '1'`

![WhatsApp Image 2025-06-11 at 11 37 46_6359fe50](https://github.com/user-attachments/assets/bd5345ec-7dbd-4ccf-aec9-59ced5c27d25)

---

## 🧰 Tools Used

* ✅ **Intel Quartus Prime**
* ✅ **ModelSim** for simulation
* ✅ **RTL Viewer** for logic diagram
* ✅ **State Machine Viewer** for state visualization

---

## 📌 How to Write FSM from Diagram

1. Draw the FSM with states and transitions
2. Define `type state_type is (A, B, C, D, E);`
3. Declare `signal state: state_type := A;`
4. Write `process(clk)` with reset and transitions using `case` block
5. Update `d_out` in transitions (Mealy-style)

---

## 👨‍💻 Author

**Sandeep Kumar**
ECE Student | Digital Design Enthusiast
🔗 [www.linkedin.com/in/sandeepkumar2612](https://www.linkedin.com/in/sandeepkumar2612)
---

## 🧠 Learnings

* FSM-based VHDL design
* Mealy vs Moore logic
* RTL synthesis and waveform simulation
* Writing clean, modular hardware description code

---

```

