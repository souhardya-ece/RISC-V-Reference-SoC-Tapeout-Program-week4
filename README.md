# RISC-V-Reference-SoC-Tapeout-Program-week4
## Circuit Design and Spice Simulation
Ckt design various component are connected in a certain format in order to perdfrom some functionality .  Generate the output wavefrom in spice simulation. A buffer have some input slew(delay) and some output load capacitance in according to that it have some value that is called delay of that buffer.

## NMOS:- 
It is a four terminal(s,d,g,b) device consists of p substrate. Therr is a isolation region beside the source and drain diffusion region and in bw them a sio2 layer on top of that there is a matal layer. Vgs>0 so negative carrier move towards interface.Depletion region get from and increase.P->N Strong inversion(the voltage at which it is occur is threshold voltage) after that 
channel width increase and the electron is move towards source to drain.Generally vsb=0 if it is positive then at the source side depletion region gets increase due to rb. e is getting pulled in source side. so we apply more vgs to invert the channel.Qi is directly proportional to vgs-vt. Now by applying Vds>0 So from s(0) to d(vds) there is an voltage gradient. So voltage at channel vgs-vx.Current=Drift curr(derivation) vds<=vgs-vt(linear region) How the Id vs vds graph will look like for different vgs we use the spice simulator.Channel Voltage-Vgs-vds.With tha increase of Vds drain side due to rb at some value of Vds at which the channel near the drain end becomes effectively pinched off(0) it is pictch off voltage.Vds>Vgs-vt at drain side there is no channel(Saturation region=> Contant current source) at that region we observe the channel length modulation. 12

## Introduction to Spice:-
Spice Model parameter Vto,gamma,kn,lamda. 
Input(spice model parameter+ Spice netlist) is feeding to the spice software we get the Wavefrom.First define nodes. like M1 d g s b . Spice netlist + Tech file.
### Simulation (Long Channel) Id vs Vds PLot
```
git colne https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
cd ~/VLSI/sky130CircuitDesignWorkshop/design
sudo apt install ngspice
ngspice day1_nfet_idvds_L2_W5.spice
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Id%20vs%20Vds_Long.png)
There is a quadratic relation bw Id and Vgs
### For Lower Node(Short Channel) Id vs Vgs Plot
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
vim day2_nfet_idvds_L015_W039.spice
ngspice day2_nfet_idvds_L015_W039.spice
plot -vdd#branch
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Id%20vs%20Vgs_Short.png)
There is a Quadratic relation of Lower vlue of Vgs if vg gets increase it will have the linear relation with Id => Velocity saturation(Lower(linear)For higher E fiels Velocity of e becomes contant deu to scattering effect) From Id vs Vds graph we get to know that the before cutoff region Id is 20 microamp and Vgs is 0.6v
Vgs-vt(min)=> Saturation; Vds(min)=> Linear Vdsat(min)=> Velocity saturation(Peak current also decrease)
### Id vs Vgs PLot(Short Channel)
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
vim day2_nfet_idvgs_L015_W039.spice
ngspice day2_nfet_idvgs_L015_W039.spice
plot -vdd#branch
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Id%20vs%20Vgs.png)
same thing we can observe over here. From this Id vs Vgs graph we get the threshold voltage is 0.77v

### VTC of CMOS
mod(vgs)>mod(vt)=>On 
mod(vgs)<mod(vt)=>Off
In Cmos When Vin=Vdd Pmos(off) and Nmos(on)=> Discharge so Vout=0; When Vin=0 Pmos(on) and Nmos(off)=> Charging so Vout=1
Vgsn-Vin;Vdsn=Vout
Vgsp=Vin-Vdd; Vdsp=Vout-Vdd
Load Curve is the Idsn Vs Vout For both Pmos and Nmos by superimposing we get the VTC
Spice Deck:-Component Connectivity and component value. Then define node and name that node. There are 4 node in Cmos inv 
From the VTC characteristic of cmos we get the switching threshold is 0.876v
### Labs
### VTC of CMOS
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
vim day3_inv_vtc_Wp084_Wn036.spice
ngspice day3_inv_vtc_Wp084_Wn036.spice
plot out vs in
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/VTC.png)
### Transiant Analysis of CMOS
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
vim day3_inv_tran_Wp084_Wn036.spice
ngspice day3_inv_tran_Wp084_Wn036.spice
plot out vs in
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Transiant.png)
From the transiant Analysis of cmos we get the rise delay(50% of vdd)=0.332s and fall delay(50% of vdd)=0.285s
### CMOS inv Robustness
1.Switching Threshold:- Vin=Vout Where the cmos cut atthat value Vm=Vin. Vgs=Vds and Idsp=-Idsn Depending upon the w/l of nmos and pmos the switching threshold will differ. When the ratio of Wp/Lp(increase) to the Wn/Ln is increase switeching threshold increase. as pmos have the more area. Rise delay decrease and fall delay increase . If the ratio is double then rise =Fall delay(This is the characteristics of clk inv)

2.Noise Margin:- If the input is in bw 0 to ViL(0) the o/p is VoH(1) and i/p is in bw viH(1) to Vdd the o/p is VoL(0); ViL>VoL and VoH>ViH  and at ViL and ViH the slope is -1 . The difference bw VoH and ViH is NMH(1) . The diff bw ViL and VoL is NML(0). The diff bw ViH and ViL is undefined region(1/0). When W/L of pmos is increase and nmos is kept contant the NMH is increase and NML is constant at cretain point. NMH and NML area are used as digital design .Undefined region is used for analog design. From the graph we We get VoH= 1.7v ViL=0.77v VoH=0.97v VoL=0.11v and NMH=0.733v NML=0.65v

### Labs
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
ngspice  day4_inv_noisemargin_wp1_wn036.spice
plot out vs in
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Vm.png)

3. Power supply Scaling:- Keeping the W/L of nmos and pmos same we vary the Vdd To find out the gain of the cmos at two -1 slope and take the dely/delx . if the Vdd goes down the gain of the cmos get increase(adv) and energy goes down(adv) and the device cannot charge and discharge properly so there is an impact on perfromance(disadv).

### Lab
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
ngspice  day5_inv_supplyvariation_Wp1_Wn036.spice
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Vary.png)
4.Device Variation:- Etching process variation. Deu to fabrication process the shape(w/L) is distorted that will impact on Id. Oxide thickness variation . Tox might not be unifrom through out the length so that will impact on id.Strong pmos (low resistence) and Weak nmos (high resistence) . so we vary the cmos to (strong pmos-weak nmos) to (weak nmos to strong nmos) the Vm decrease and NM decrease .

We vary all the static thing still the operation of cmos is kept intact.
###Lab
```
cd ~/VLSI/sky130CircuitDesignWorkshop/design
ngspice  day5_inv_devicevariation_wp7_wn042.spice
plot out vs in
```
### Output
![image alt](https://github.com/souhardya-ece/RISC-V-Reference-SoC-Tapeout-Program-week4/blob/main/Images/Device.png)



