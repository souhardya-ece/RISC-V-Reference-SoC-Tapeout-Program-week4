# RISC-V-Reference-SoC-Tapeout-Program-week4
## Circuit Design and Spice Simulation
Ckt design various component are connected in a certain format in order to perdfrom some functionality .  Generate the output wavefrom in spice simulation. A buffer have some input slew(delay) and some output load capacitance in according to that it have some value that is called delay of that buffer.

## NMOS:- 
It is a four terminal(s,d,g,b) device consists of p substrate. Therr is a isolation region beside the source and drain diffusion region and in bw them a sio2 layer on top of that there is a matal layer. Vgs>0 so negative carrier move towards interface.Depletion region get from and increase.P->N Strong inversion(the voltage at which it is occur is threshold voltage) after that 
channel width increase and the electron is move towards source to drain.Generally vsb=0 if it is positive then at the source side depletion region gets increase due to rb. e is getting pulled in source side. so we apply more vgs to invert the channel.Qi is directly proportional to vgs-vt. Now by applying Vds>0 So from s(0) to d(vds) there is an voltage gradient. So voltage at channel vgs-vx.Current=Drift curr(derivation) vds<=vgs-vt(linear region) How the Id vs vds graph will look like for different vgs we use the spice simulator.Channel Voltage-Vgs-vds.With tha increase of Vds drain side due to rb at some value of Vds at which the channel near the drain end becomes effectively pinched off(0) it is pictch off voltage.Vds>Vgs-vt at drain side there is no channel(Saturation region=> Contant current source) at that region we observe the channel length modulation. 12

## Introduction to Spice:-
Spice Model parameter Vto,gamma,kn,lamda. 
Input(spice model parameter+ Spice netlist) is feeding to the spice software we get the Wavefrom.First define nodes. like M1 d g s b . Spice netlist + Tech file.
### Simulation 
```
git colne https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
cd ~/VLSI/sky130CircuitDesignWorkshop/design
sudo apt install ngspice
ngspice day1_nfet_idvds_L2_W5.spice
```


