## Easy Custom Device Tool ##

**Easy Custom Device Tool** provides a LabVIEW developer  an easy way to create custom devices for NI VeriStand. Using this tool, one can create a custom device without knowing any custom device specific development details. The tool will abstract all the custom device details from the developer, letting them focus on the functionality.

Due to the abstraction, a developer can create a custom device in a fraction of the time typically required. However, much of the advanced functionality of custom devices will be unavailable.

To use the tool, first generate a blank custom device with the custom device template tool that ships with NI VeriStand. Then, run the provided Edit Custom Device Project.vi to modify it into the Easy Custom Device Framework. An example walkthrough is provided in a separate document.

After creating the custom device project, the developer can implement their functionality by modifying the strict type defined controls and the provided custom device VIs.

### LabVIEW Version ###

LabVIEW 2010

### Quality, Limitations ###

This tool was developed against LabVIEW 2010 and NI VeriStand 2010. It has been used several times since without issues, but is vulnerable to a future NI VeriStand custom device template tool change breaking this tool. Therefore, it may or may not work forever.

### License ###

*This repository and any materials provided by NI therein are provided AS IS. NI DISCLAIMS ANY AND ALL LIABILITIES FOR AND MAKES NO WARRANTIES, EITHER EXPRESS OR IMPLIED, INCLUDING WITHOUT LIMITATION ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR  PARTICULAR PURPOSE, OR NON-INFRINGEMENT OF INTELLECTUAL PROPERTY. NI shall have no liability for any direct, indirect, incidental, punitive, special, or consequential damages for your use of the repository or any materials contained therein.*

## Easy Custom Device Framework ##
### Strict Type Defined Controls  ####
#### Configuration Data  ####
This cluster contains the data that you want to the user to configure from the NI VeriStand System Explorer. It will be displayed in the System Explorer for the user to configure. Items in this cluster could include run time settings like file paths, hardware names, and so on. 

#### Channel Data ####
This cluster contains the data that the NI VeriStand engine must access as channels. It contains a cluster of Inputs and a cluster of Outputs. The controls in this cluster are added as channels in the System Explorer under the custom device. They represent the inputs and outputs of the custom device at run-time.

#### Real-Time System Data ####
This cluster contains data or references that are used during the execution of the VeriStand engine. Place any references that you need to use at run-time, as such file references or DAQmx tasks. 

### Custom Device VIs ###
#### Init VI ####
Once the custom device is deployed and running on the VeriStand engine, this is the first VI to execute. It should initialize values, set up tasks, or open references. 

#### Start VI ####
This VI executes before the looping structure of the custom device. It should start any tasks that must begin before the loop. 

#### Sub VIs ####
If you will be using sub-VIs in your custom device, the sub-VIs need to be added to the Custom Device library created for your custom device. Adding the sub-VIs to this library includes the VI in the libraries namespace, allowing VIs of the same name to be used across multiple custom devices.  

#### Execute VI ####
This VI executes within the looping structure of the custom device. Each iteration, the latest value of the custom device input channels are provided to this subVI in the channel data cluster. The Execute VI can write these input values to hardware, log them to file, or perform other operations on the data. After the Execute VI finishes, the output values in the channel data cluster are used to update the output channels of the custom device.

#### Stop VI ####
This VI executes when the custom device is stopped. It should close references, resolve errors, and perform shut-down tasks. 