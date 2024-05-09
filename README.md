<img src="https://github.com/contiki-ng/contiki-ng.github.io/blob/master/images/logo/Contiki_logo_2RGB.png" alt="Logo" width="256">

# Contiki-NG: The OS for Next Generation IoT Devices

[![Github Actions](https://github.com/contiki-ng/contiki-ng/workflows/CI/badge.svg?branch=develop)](https://github.com/contiki-ng/contiki-ng/actions)
[![Documentation Status](https://readthedocs.org/projects/contiki-ng/badge/?version=master)](https://contiki-ng.readthedocs.io/en/master/?badge=master)
[![license](https://img.shields.io/badge/license-3--clause%20bsd-brightgreen.svg)](https://github.com/contiki-ng/contiki-ng/blob/master/LICENSE.md)
[![Latest release](https://img.shields.io/github/release/contiki-ng/contiki-ng.svg)](https://github.com/contiki-ng/contiki-ng/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/contiki-ng/contiki-ng.svg)](https://github.com/contiki-ng/contiki-ng/releases/latest)
[![Last commit](https://img.shields.io/github/last-commit/contiki-ng/contiki-ng.svg)](https://github.com/contiki-ng/contiki-ng/commit/HEAD)

[![Stack Overflow Tag](https://img.shields.io/badge/Stack%20Overflow%20tag-Contiki--NG-blue?logo=stackoverflow)](https://stackoverflow.com/questions/tagged/contiki-ng)
[![Gitter](https://img.shields.io/badge/Gitter-Contiki--NG-blue?logo=gitter)](https://gitter.im/contiki-ng)
[![Twitter](https://img.shields.io/badge/Twitter-%40contiki__ng-blue?logo=twitter)](https://twitter.com/contiki_ng)


### Installation Instructions for LSM-RPL GitHub Source Code

**Introduction:** 

Contiki-NG is an open-source, cross-platform operating system for Next-Generation IoT devices. It focuses on dependable (secure and reliable) low-power communication and standard protocols, such as IPv6/6LoWPAN, 6TiSCH, RPL, and CoAP. Contiki-NG comes with extensive documentation, tutorials, a roadmap, release cycle, and well-defined development flow for smooth integration of community contributions.

LSM-RPL, or Lightweight Security Mode RPL, is a security enhancement for the Routing Protocol for Low-Power and Lossy Networks (RPL) within the Contiki-NG environment. This innovative technique focuses on bolstering the integrity and authenticity of RPL control messages, crucial for safeguarding IoT networks against various external and internal threats. 

The key tenets of LSM-RPL involve the utilization of secret keys - a private key (Kpr) and a shared key (Ksh) - assigned to individual sensor nodes. These keys serve as the foundation for authenticating RPL control messages, thereby fortifying the network against unauthorized access and manipulation by external adversaries. Moreover, LSM-RPL employs Hashed Message Authentication Code (HMAC) techniques to sign RPL control messages, ensuring both their integrity and authenticity during transmission. 

By appending HMAC digests to these messages, LSM-RPL provides a robust mechanism for detecting and thwarting various forms of attacks, such as version and rank manipulation, which could compromise the stability and reliability of the RPL network. 

These instructions guide you through the process of setting up and testing LSM-RPL on your system.

**Prerequisites:**

Ensure Contiki-NG OS and Cooja simulator are installed and functioning correctly.

**System Setup Verification:**

1. Ensure that Contiki-NG OS and the Cooja simulator are installed and fully operational on your system.
2. Launch the Cooja simulator.
3. Open an existing simulation project to confirm functionality. For example, navigate to "\home\user\contiki-ng\examples\rpl-udp" and run the "rpl-udp-cooja.csc" file.
4. If the simulation project runs without errors, it indicates that both Contiki-NG OS and the Cooja simulator are correctly installed and operational, and you're ready to proceed with using LSM-RPL.

**Install and Test RPL-LSM:**

1. Copy the "LSM.rar" file to the directory "\home\user\contiki-ng".
2. Extract the contents of the "LSM.rar" file into the same directory.
3. When prompted, select "Yes to all" to replace existing Contiki-NG files with the updated code.
4. Launch the Cooja simulator.
5. Navigate to the directory "\home\user\contiki-ng\LSM-example\Visualization\15_nodes_LSM".
6. Attempt to open the simulation project named "cooja.csc".
7. If the simulation project opens and runs without errors, congratulations! The installation of LSM-RPL was successful.

**Activation and Deactivation of LSM-RPL:** 

1. Open the "project-conf.h" file located within the project directory.
2. Locate the macro named "CONF_LSM".
3. Set the value of "CONF_LSM" to either 1 or 0 to activate or deactivate security protection using LSM-RPL, respectively.
   ```c
   #define CONF_LSM 1 // Lightweight Security Mode
   ```

**Activating Specific Attacks:**

1. **Enable Attack Macros:**
   - Open the "project-conf.h" file located within the project directory.
   - Enable the corresponding macros related to the desired attacks by setting them to 1.
   ```c
   #define CONF_SFA 0 // Selective Forward Attack
   #define CONF_VNA 0 // Version Number Attack
   #define CONF_DRA 0 // Decrease Rank Attack
   #define CONF_IRA 0 // Increase Rank Attack
   ```

2. **Set Attack Parameters in JavaScript Control Code:** 
   - Open the "coojalogger.js" file that manages simulation execution in Cooja.
   - Define the start and end time of the attack, as well as the number of target nodes, using the provided syntax.
   ```javascript
   attacks.push(new Attack("DRA_on", 16, 1, 3600000)); // Activate DRA for node 16 for 1 hour
   attacks.push(new Attack("VNA_on", 17, 1, 3600000)); // Activate VNA for node 17 for 1 hour
   ```


## Comparing Network Scenarios

### Set Network Parameters:
To compare network scenarios, adjust the network parameters for each scenario according to your requirements.

### Run Network Simulation in Cooja No-GUI Mode:
Execute the network simulation in Cooja's no-GUI mode using the provided Python script "run-cooja.py".
Run the script in the terminal as follows:
```bash
python3 run-cooja.py
 ```
The "run-cooja.py" script will execute the simulation file named "cooja.csc" and generate a log file named "COOJA.testlog" containing all the logs and events that occurred during the simulation.

### Extract Network Performance Evaluation from Log File:
From the generated log file ("COOJA.testlog"), extract all network performance evaluation metrics as explained in the next section.

Repeat the Steps for Different Scenarios:
Repeat the above steps with different network parameters, such as varying the number of malicious nodes, to generate different log files for comparison.
