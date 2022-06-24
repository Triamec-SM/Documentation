This user guide describes how to set up the **TSD and TSP** servo drive
series.

# <span id="anchor"></span>Abbreviations

|         |                                       |
|---------|---------------------------------------|
| AC      | Alternating Current                   |
| DC      | Direct Current                        |
| HMI     | Human-Machine Interface               |
| LED     | Light Emitting Diode                  |
| PC      | Personal Computer                     |
| STO     | Safe Torque Off                       |
| TAM     | Triamec Advanced Motion               |
| TAM API | TAM Application Programming Interface |

# <span id="anchor-1"></span>Introduction

This user guide describes how to set up the **T**SD** and **TSP** servo
drive series.

After a short description of the required hardware and software setup in
chapter [2](#anchor-2), the user guide explains the usage of the **TAM
System Explorer** software in chapter [3](#anchor-3) and [4](#anchor-4).
**Chapter [5](#anchor-5) describes the commissioning and tuning of a
servo axis.** Chapter [6](#anchor-6) handles several advanced topics and
chapter [7](#anchor-7) explains the **Tria-Link** observer.

To control Triamec drives with **Beckhoff Twin**CAT**, first setup the
drives as described in this document. Then proceed to document
[\[2\]](#anchor-8) for a **Tria-Link** setup, or [\[3\]](#anchor-9) for
an **EtherCAT **setup.

Names in italics, like **Triamec**, are general keywords. Register names
and paths are indicated according to the following example:
Axes\[0\].Parameter.PositionController.OutputLimit.** Bold expressions
indicate a**n** **HMI** item, **i.e.** ******File ****\>**** Open****.
Keyboard keys are formatted like **Enter**.

This user guide prerequisites the use of a TAM System Explorer version ≥
7.19 and a drive firmware ≥ 4.15.

# <span id="anchor-2"></span>Hardware and Software Setup

This chapter describes the hardware prerequisites and the installation
of the required software used for commissioning of the drive.

## <span id="anchor-10"></span>Hardware Prerequisites

For the commissioning of the Triamec drive with this user guide the
following hardware setup is required.

-   A motor with an encoder connected to the drive.
-   The DC-bus is supplied with an appropriate DC voltage using a
    Triamec power supply.
-   The drive logic is supplied with 24VDC.
-   Make sure the STO channels are connected correctly to fulfill the
    safety requirements.
-   Connect the drive with the PC (see section [2.1.1](#anchor-11) for
    further information).

See also the corresponding hardware manual for further information:

-   [www.triamec.com](http://www.triamec.com/) ****\>****
    ****Support**** ****\>**** **Documents** ****\>**** Manuals**** ****
-   ****o****r ****Help \> Documentation \> Hardware**** in ******TAM
    System Explorer******.****

### <span id="anchor-11"></span>Connecting the drive with the PC

For the commissioning of the drive, the following options are available
to connect the drive with the PC:

##### USB

-   Connect the drive to the PC with a **USB** cable. Multiple drives
    can be connected together to the PC by using a **USB** hub.

-   An existing **Tria-Link **network can be connected with an
    (external) **PC** via **USB** either

    -   by using a **USB-Tria-Link** adapter module (**TLU**)
    -   or by connecting the **PC** to the adapter card as described in
        chapter [7](#anchor-7)

In case a Windows Explorer window opens when the drive is rebooted or
when USB is connected to the PC, this can be suppressed by changing the
following Windows settings:

-   **Windows Start Button** – **Settings** (gear wheel) – **Auto Play**
-   Under **Removable drive** select **Take no action** from the
    pull-down menu.

##### Ethernet

-   See document [\[4\]](#anchor-12) on how to set up an **Ethernet**
    connection.

##### Tria-Link

-   **Tria-**L**ink** requires a **Tria-**L**ink **PCI a**dapter
    car**d** installed on the **PC**.

-   All *Tria-*L*ink* devices must build a ring network which is
    connected to the adapter card.

-   The adapter card can be used either with a control system or with
    *TAM System Explorer,* but not both at the same time. To access the
    drives with *TAM System Explorer* while *TwinCAT* is running, use an
    additional USB or Ethernet connection to the drives.

-   To grant the *TAM System Explorer* access via PCI, Go to **File \>
    Preferences \> Startup \> Acquired Adapters** and set one of the
    following values:

    -   Triamec devices over PCI
    -   Triamec devices w/o Ethernet
    -   All Triamec devices

-   Remark: **Tria-**L**ink** is *not* supported with **EtherCAT**
    drives.

## <span id="anchor-13"></span>Software Installation

For the commissioning of **Triamec** drives **TAM System Explorer** is
required. **TAM System Explorer** provides access to the drive
parameters, commands and signals. Additional tools are available for
measuring signals, identifying the dynamic behavior and tuning the
controllers. **TAM System Explorer** is an application based on **TAM
*API* and is installed as part of the **TAM *Software* package.
Administrator rights are required during the installation process. The
following steps describe how to run the installation:

1.  Download the current release of **TAM *Software* **from
    **www.triamec.com** ****\>**** Support ****\>**** TAM Software****.
2.  Extract the downloaded ZIP file and run the installer *TAM Software
    \*.\*.\* Setup.exe*.
3.  The ****TAM **Software** Setup**** dialog is opened (Figure 1).
    Click ****Install**** to start the installation process.
4.  If a ****User Account Control**** dialog is opened check if the
    verified publisher is correctly identified as **Triamec Motion AG**
    and acknowledge the installation process.
5.  The setup process will also install the required drivers. Additional
    prompts might appear during this process which need to be approved.
6.  <img
    src="gitbook/Pictures/Pictures/100000010000025800000175EBB441FFE17D68F1.png"
    title="fig:" style="width:8.999cm;height:5.636cm"
    alt=" Figure 1: TAM Software Setup" />In some cases a restart of the
    *PC* is required to complete the installation process. In this case,
    a prompt will pop up with the request to restart the *PC*.

> ****Note ****In some side-by-side installation scenarios, uninstalling
> the **TAM *Software* might fail. In such a case, first **repair** the
> software, then **uninstall**.

> ****Note**** Uninstalling the **TAM *Software* might also remove the
> associated device drivers. In this case all programs accessing Triamec
> devices may fail.

# <span id="anchor-3"></span>How to use TAM System Explorer

This chapter gives an introduction into the usage of **TAM System
Explorer**.

If **TAM *Software* is installed correctly **TAM System Explorer** can
be executed from the ****Windows Start Menu****. Figure shows the window
after the start, containing the following panels:

1.  **Topology Tree**: The topology tree allows to navigate between
    different devices and registers.
2.  **Axis Monitor**: The axis monitor shows the state for each axis and
    allows to acknowledge pending errors. Additionally, emergency
    buttons are provided.
3.  *Scope*: The scope allows to plot the values of all registers
    provided by the topology tree.
4.  **Tab Panel**: The tab panels are used to write and read to
    registers from the **Topology Tree**, to set the scope properties
    and to log messages.

<figure>
<img
src="gitbook/Pictures/Pictures/2000005E00004A38000031FDBDD2F08B7C8C079D.svm"
style="width:18.002cm;height:12.12cm"
alt=" Figure 2: TAM System Explorer after start up. 1: Topology Tree; 2: Axis Monitor; 3: Scope Window; 4: Tab Panel" />
<figcaption aria-hidden="true"><br />
Figure 2: TAM System Explorer after start up. 1: Topology Tree; 2: Axis
Monitor; 3: Scope Window; 4: Tab Panel</figcaption>
</figure>

## <span id="anchor-14"></span>Topology Tree

After an initializing phase, the** **T**opology **T**ree** shows the
actual hardware content of the system. The **Topology Tree** is built
out of the following objects:

|                                                                              |                        |                                                                                                                                       |
|------------------------------------------------------------------------------|------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <img                                                                         
 src="gitbook/Pictures/Pictures/1000000100000010000000105CBF1ABE07E862DC.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Local Computer         | Computer on which the **TAM System Explorer** is running                                                                              |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010EE2A24D77741BDBF.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Tria-Link Adapter Card | **PCIe** adapter card used to communicate over **Tria-Link**.                                                                         |
| <img                                                                         
 src="gitbook/Pictures/Pictures/10000001000000100000001047AD1D04D65E8FA9.png"  
 style="width:0.42cm;height:0.42cm" />                                         | USB Adapter            | Adapter if **USB** is connected to a **TLO** card, an **Ethernet** to **USB** adapter or if **USB** is directly connected to a device |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010C551E56FFD0B7EA4.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Ethernet Adapter       | Used to communicate over **Ethernet**                                                                                                 |
| <img                                                                         
 src="gitbook/Pictures/Pictures/10000001000000100000001059F8E935C5AB163C.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Tria-Link              | **Tria-Link** communication channel used to connect the adapter with devices                                                          |
| <img                                                                         
 src="gitbook/Pictures/Pictures/10000001000000100000001030D2D618D9ECE114.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Tria-Link Observer     | **Tria-Link** communication channel in observer mode (see chapter [7](#anchor-7))                                                     |
| <img                                                                         
 src="gitbook/Pictures/Pictures/1000000100000010000000103685E167FFEAF347.png"  
 style="width:0.423cm;height:0.423cm" />                                       | Station                | Addressable node within the link                                                                                                      |
| <img                                                                         
 src="gitbook/Pictures/Pictures/1000000100000010000000109BAE6FE6F7D7B810.png"  
 style="width:0.423cm;height:0.423cm" /> <img                                  
 src="gitbook/Pictures/Pictures/100000010000001000000010FD39DBAF3F16ECEF.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Device                 | Logical unit providing a register tree, for example a servo drive                                                                     |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010AB22FA745AD1A8F2.png"  
 style="width:0.42cm;height:0.42cm" /> <img                                    
 src="gitbook/Pictures/Pictures/1000000100000010000000108621CD3A8466C083.png"  
 style="width:0.423cm;height:0.423cm" />                                       | Register Node          | Collection of registers with similar purpose (array of similar structures)                                                            |
| <img                                                                         
 src="gitbook/Pictures/Pictures/10000001000000100000001021656958D347E96B.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Register               | Representing a parameter, a command, a signal or information                                                                          |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010DE168281BBDD696A.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Register Array         | An array of registers of the same type                                                                                                |
| <img                                                                         
 src="gitbook/Pictures/Pictures/1000000100000010000000108C92A8DAC7412EA9.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Tama Manager           | Allows to assign, download and enable **Tama** programs                                                                               |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010BF7749A038E43931.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Module                 | User interfaces which simplify the register access e.g. for the tuning of the axes.                                                   |
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000001000000010297828A6A3E1230E.png"  
 style="width:0.42cm;height:0.42cm" />                                         | Option Module          | Option module for additional input and output.                                                                                        |

****Note ****If a connected device is not listed in the **Topology
Tree**, execute a restart (**File \| Restart**).

If a device is connected via **USB** or **Ethernet** and a LinkNotReady
warning occurs, set register General.Parameters.Standalone* *to TRUE.

It is recommended to give the stations a meaningful name e.g. **Station
XY**, **Station Z**. The naming of the station can be changed by
selecting the station and then clicking the station name or pressing
**F2**. The station name is stored in register
General.Parameters.DeviceName. The hardware device related to the
station can be identified either

-   by the serial number which is displayed in the tab panel under
    **General \> Device Serial Number**
-   or by activating the status **LED** (red blinking) of the drive by
    setting General.Commands.ExternalError* *to TRUE.

Each device in the **Topology Tree** provides a **Register Tree**. The
**Register Tree** is the basic interface between **TAM System Explorer**
and the device. The registers are divided into four classes:

-   Parameters
-   Commands
-   Signals
-   Information

In order to interact with a register** **unfold the **Topology Tree**
until the desired register gets visible. The registers may be hidden, to
reduce vertical amount of space occupied by the tree. In order to show
them, click on the ****Show/Hide individual registers**** Button .

<img
src="gitbook/Pictures/Pictures/100000000000036A00000246D5BFE9D7A9533581.png"
title="fig:" style="width:18.002cm;height:11.989cm"
alt=" Figure 3: TAM Topology Tree and Registers" />A click on a register
node or a register opens the ****Register****** **tab in the tab panel.
All registers contained in the selected register node are listed in the
register panel.

### <span id="anchor-15"></span>Parameters

Parameters are used to configure the drive for the intended application,
e.g. to set up the position controller or the encoder. Typically, a
parameter value is written when commissioning the drive and remains
unchanged, except if the system is changed. Parameters can be stored in
a configuration file on the PC or persisted on the drive (see sections
[3.5](#anchor-16)).

In the ****Register****** **tab in the tab panel the parameters are
listed with the following columns:

-   Register → the name of the register, corresponding to the name in
    the tree
-   Actual → the actual register value stored on the drive
-   Prepare → the register value which will be written to the drive
    after clicking ****Commit***** *
-   Unit* *→ physical unit of the value
-   Description → short description of the parameter

Only the prepare field is editable. If the prepare value has a gray
background, the register is read only. A changed value gets an orange
background. This state remains until it gets committed.

Parameter handling buttons:

|                                                                              |                |                                                                    |
|------------------------------------------------------------------------------|----------------|--------------------------------------------------------------------|
|  <img                                                                        
 src="gitbook/Pictures/Pictures/1000000100000010000000101F11ECF580CA628E.png"  
 style="width:0.42cm;height:0.42cm" />                                         | ****Commit**** | Updates the drive with the values of the prepare fields.           |
|  <img                                                                        
 src="gitbook/Pictures/Pictures/100000010000001000000010D30201F0070FFE0E.png"  
 style="width:0.42cm;height:0.42cm" />                                         | ****Revert**** | Reverts the prepare fields with the values from the actual fields. |

Setting a parameter value:

1.  Enter the desired value into the prepare field of the appropriate
    register
2.  Press **Enter** or click into another register. The background of
    the edited field gets orange.
3.  Click the ****Commit**** button to transmit the value to the drive.
    After a successful commit, the background of the prepare field turns
    back to white.

A star (**\***) in front of a tree item indicates an uncompleted commit.

### Commands

Commands are used to change the state of the device, e.g. to set a
digital output or to execute a move. The state of a command can not be
stored and will be reset after a restart of the device.

In the tab panel commands are listed with the following columns:

-   Register → the name of the register, corresponding to the name of
    the tree view
-   Value → the actual value of the command
-   Unit* *→ physical unit of the value
-   Description → short description of the command

Command values can be edited directly, no commit command is required to
execute the command:

1.  Enter the desired value into the value field of the appropriate
    register.
2.  Press **Enter** or click into another register to execute the
    command.

### Signals

Signals allow real time observation of the state of the drive.

In the tab panel signals are listed with the following columns:

-   Register → the name of the register, corresponding to the name of
    the tree view
-   Value → the actual value of the signal
-   Unit* *→ physical unit of the value
-   Description → short description of the register

All signals are read only.

### <span id="anchor-17"></span>Information

Information registers can be used to document the properties of an axis.
They do not affect the behavior of the drive in any way. Information
registers are also stored with the TAM configuration file on the PC or
persisted on the drive (see sections [3.5](#anchor-16)).

****Note ****The register Axes\[\].Informaton.AxisName is used by the
axis monitor, the scope and the modules to display the axis
identification.

## <span id="anchor-18"></span>Axis Monitor

Below the **T**opology **T**ree** the axes are listed in the axis
monitor as a flat list.

The axes are identified by the register Axes\[\].Information.AxisName.
Initially the station name is added in front of AxisName, but will be
removed when the axis name is changed the first time.

<img
src="gitbook/Pictures/Pictures/1000000100000172000000D0270B32677DE474B7.png"
title="fig:" style="width:9.264cm;height:5.211cm"
alt="Figure 4: The axis monitor shows the state for each axis and allows to acknowledge pending errors. Additionally, the emergency buttons are provided." />The
axis name can be changed by selecting the axis name in the axis monitor
and clicking it again or by pressing **F2 **. The modified axis name is
also stored in the register Axes\[\].Information.AxisName.

The axes are highlighted according to their state:

-   **Enabled:** Enabled axes are marked with a green square.
-   **Error:** If an axis has a problem, the axis is marked with an
    error icon. The error type is shown in the ****State**** column,
    highlighted in red. Resolved errors don't simply disappear. They
    need to be acknowledged using the  Acknowledge Errors button. If no
    errors are pending for acknowledgment, this button is grayed out.
-   **Warning:** Orange state color indicates a warning.

Warnings as well as errors which can't yet be acknowledged need some
interaction, for example providing the required DC bus voltage in case
of a DcBusVoltageOutOfRange warning.

The ****Control system overridden**** column shows a slowly blinking 👷
icon on orange background as long as an axis module is attached (see
chapter [4.1](#anchor-19)).

The ****A****sy VM**** and ****I****so VM**** columns reflect the states
of the asynchronous and isochronous **Tama** virtual machines (see
chapter [3.7](#anchor-20)). Different characters are shown depending on
the state.

|           |                                                  |
|-----------|--------------------------------------------------|
| Character | Meaning                                          |
| (empty)   | There is no Tama program on the device           |
| ⬛        | The virtual machine is not operational           |
| ▶         | The virtual machine is operational               |
| \-        | The state is not retrieved and therefore unknown |

In case of a communication failure, the state of a device can be shown
as Unresponsive, or even as Link down, if the entire link is broken.

****Caution**** In some cases[^1] the communication between the **Axis
M**onitor** and the drive could be suspended. In these cases, the axis
state is probably not reflected correctly. Check the registers
General.Signals.DriveState and Axes\[\].Signals.General.AxisState
instead or restart **TAM System Explorer **(****File ****\>****
Restart****).

The axis monitor also provides two emergency buttons:

|                                                                              |                                                                                                                                                                                                                                                                                                                                    |
|------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img                                                                         
 src="gitbook/Pictures/Pictures/100000010000003000000030C957B26EE2485D8D.png"  
 style="width:0.72cm;height:0.72cm" />                                         | **Emergency switch off**: All power sections will switch off immediately if this button is pressed. The axes are then released and may move until the kinetic or potential energy is dissipated. Pressing the emergency button will cause an external error which has to be reset e.g. by pressing the  Acknowledge Errors button. |
| <img                                                                         
 src="gitbook/Pictures/Pictures/1000000100000030000000303B422D589D13367C.png"  
 style="width:0.718cm;height:0.718cm" />                                       | **Emergency Stop**: If emergency stop is pressed, the path planner will issue a stop move based on the emergency parameters. This brings all active axis to a halt. The axes will remain enabled.                                                                                                                                  |

****Caution**** ****Switching off the power section of a drive during
motion may damage the mechanical axis.

## <span id="anchor-21"></span><span id="anchor-22"></span>Scope

The scope is a very powerful tool with a lot of functionalities. It
allows to plot all register items (signals, parameters, commands) with a
sampling rate of up to 100kHz. To add a new register item to the scope,
simply drag it from the **Topology Tree** and drop it into the scope
area (see also Figure ).

****Remarks**** ****Dragging and dropping of signals is not possible
while the scope is running.

Registers from a **second** drive can only be added (drag and drop) when
the two drives are synchronized (e.g. if they use the same link).

**** ****If the registers are not shown in the **Topology Tree******
****click**** the ****Show/Hide individual registers**** Bu****tton
****.****

Scope settings can be set by opening the scope tab in the tab panel**
**(see section [3.3.1](#anchor-23)). Controls related to the scope can
be found either

-   in the scope menu in the main menu bar,
-   in the scope tool bar
-   or by opening the context menu with a right click on the scope area.

### <span id="anchor-23"></span>Scope Settings

To modify the scope settings, click the ****Scope**** tab in the tab
panel or click the scope area to activate the ****Scope**** tab. At the
right, the list of registers (called **Plots**) assigned to the scope is
shown. On the left, the tabs with the scope settings are displayed. The
scope settings are divided into three groups:

-   The ****General**** tab specifies scope properties valid for all
    plots.
-   The ****Plot**** tab specifies the properties of the currently
    selected plot.
-   The ****Cursor**** tab owns the properties of the two cursors and
    the trigger.

To remove a plot from the scope, select the plot in the plot list and
press **Delete** or click the ****Delete the selected plot(s)**** button
.

****Remark ****Scope settings can only be modified while the scope is
not running.

### Sampling Time

The default sampling time is one millisecond. The sampling time can be
increased or decreased by changing the ****Default Sampling Time**** in
the ****General**** tab for all signals or by changing the ****Sampling
Time**** in the ****Plot**** tab for individual signals (Figure and ).
The following sampling times are supported: 0.01ms, 0.02ms, 0.1ms and
multiples of 0.1ms. Unsupported values will be rounded to the next valid
sampling time.

The maximal number of values which can be received from a drive depends
on the sampling time and the data type of the register. Most registers
contain 32-bit values, only absolute positions without a 'Float'
identifier are 64-bit values. The following table shows the maximum
number of plots depending on the sampling time and the register type:

|         |        |        |
|---------|--------|--------|
| 0.01    | 8      | 4      |
| 0.02    | 16     | 8      |
| 0.1     | 80     | 40     |
| 0.1 · n | 80 · n | 40 · n |

<img
src="gitbook/Pictures/Pictures/10000001000001DB000000B8F599838852437795.png"
title="fig:" style="width:10.68cm;height:4.03cm"
alt=" Figure 6: Scoping Error" />When the maximal number of plots is
exceeded, an error message will pop up (Figure ). In this case the
number of plots must be reduced or the sampling time increased.

****

****Remarks****** **A large number of plots with small sampling time
will cause a huge data stream. Depending on the performance
characteristic of the PC this could severely reduce the responsiveness
of** **TAM System Explorer**, especially if expensive plot styles are
used e.g. if** ******Plot \> Apearance \> ****PointStyle**** is
different from** ******None******.**

** **Other applications using the same link (e.g TwinCat) can reduce the
maximum amount of registers which can be plotted.

### Sampling Duration

<img
src="gitbook/Pictures/Pictures/10000000000001EF0000010497419817D6407FB0.png"
title="fig:" style="width:9.8cm;height:5.249cm"
alt=" Figure 7: Sampling duration and multiple Y axes." />The sampling
duration can be set by clicking on the minimum/maximum label of the time
axis in the scope (Figure ). The unit of the time axis is millisecond.

****Remark****** **Long sampling duration and small sampling time with a
large number of plots will cause a huge amount of data. Depending on the
characteristic of the PC this could cause memory issues, especially on
32 bit PCs.

**

### Y Axes

Y axes can be created, edited and removed by opening the ****YAxis
Collection Editor**** by clicking ****General \> YAxis \> **** ****in
the ****Scope**** tab (see also Figure ).

-   Use ****Appearance \> Caption**** to name the axis.

****To assign a ****plot**** to ****an existing**** ****axis, select the
****plot**** in the ****plot**** list and assign the axis with the
****pull-down menu from**** ****Plot \> Axes \> YAxis****.

Y range:

-   ****The min/max range of an axis can also be changed by clicking on
    the min/max axis label (****Figure**** ****). ****
-   Clicking on the upper part of a Y axis will scale into the range,
    clicking on the lower part scales out.
-   ****The Y axis has a context menu ****(click right on the axis)
    ****with entries to achieve the same effect. ****
-   You can also move plots up and down by dragging their Y axis.
-   ****Use the ****center ****button **** to vertically center the
    selected plot.****

****The scope always ****activates**** the Y grid of the Y axis
****that**** the mouse hovered over ****last****. The Y grid is also
adjusted when hovering over a plot in the ****plot**** list****.
****This can be disabled by making a ****Y ****grid sticky ****with the
context menu of the axis**** as shown in ****Figure**** ****.****

<table>
<tbody>
<tr class="odd">
<td><img
src="gitbook/Pictures/Pictures/10000000000001A3000001057372D14F0E3CEE30.png"
title="fig:" style="width:8.405cm;height:5.233cm"
alt=" Figure 8: Changing the Y axis range." /></td>
<td><img
src="gitbook/Pictures/Pictures/100000000000009F000000664DF7FF83AD993E64.png"
title="fig:" style="width:4.2cm;height:2.701cm" alt=" " /></td>
</tr>
</tbody>
</table>

### Triggering

To start scoping press the ****Start**** button . By default the scope
is in single trigger mode . For automatic triggering click to toggle to
repeat mode or set the parameter ****General \> ScopeCharting****** **to
****True****.

**Signal trigger:** It is also possible to use a signal from the plot
list as a trigger source. The following steps are required to setup a
signal trigger:

1.  <img
    src="gitbook/Pictures/Pictures/1000000000000090000000A5A907D25EA2398D92.png"
    title="fig:" style="width:3.81cm;height:4.366cm"
    alt=" Figure 10: Trigger mode." />Select a trigger mode from the
    ****Select t****rigger****s**** pull-down menu (Figure ):
2.  Assign the trigger signal to the ****Plot**** property in the
    ****Cursor**** tab by selecting the desired plot from pull-down
    menu**** ****(see also Figure ).
3.  Set the desired trigger level to the**** Level ****property in the
    ****Cursor ****tab.
4.  To define the pre-trigger and the post-trigger duration set ****Axes
    \> T****imeAxis \> Range \> Minimum/Maximum**** in the ****Plot****
    tab or click on the min/max label of the time axis (Figure ).
5.  The scope shows a red draggable cross-hair which can be used to set
    the trigger level and the trigger time.
6.  Press the ****Start**** button to activate the trigger.

<!-- -->

1.  

|                                                                                                          |                                                                                                                                                                              |                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img                                                                                                     
 src="gitbook/Pictures/Pictures/10000001000001120000019C31AFCBBF40D9D10A.png"                              
 style="width:4.987cm;height:7.47cm" />                                                                    | <img                                                                                                                                                                         
                                                                                                            src="gitbook/Pictures/Pictures/10000001000001130000016AFB40B796A2B434FB.png"                                                                                                  
                                                                                                            style="width:5.593cm;height:7.361cm" />                                                                                                                                       | <img                                                                                                                                                                                                           
                                                                                                                                                                                                                                                                                           src="gitbook/Pictures/Pictures/100000000000018100000208D8012CDD8A5BCCED.png"                                                                                                                                    
                                                                                                                                                                                                                                                                                           style="width:6.435cm;height:9.126cm" />                                                                                                                                                                         |
| Figure 11: General tab of the scope. The most commonly used parameters are Default Sampling and YAxes*.* | Figure 12: Plot tab of the scope. The most commonly used parameters are LineColor, Name and Sampling Time*. Selecting several plots allows for configuring them altogether.* | *Figure : Repeat and trigger buttons. A horizontal draggable line marks the trigger level, the vertical draggable line defines the time of the trigger event. The *Plot* property defines the trigger source.* |

It is possible to store the data of each trigger event automatically to
a file on the **PC** with **Auto-Save**. Auto-save mode can be activated
by clicking the pull-down-menu to the right of the repeat icon and
select ****Auto-Save****. When auto-save is active, the repeat icon
shows a small blue disc symbol . The auto-saved data from the trigger
events can be accessed from TAM System Explorer by clicking ****File \>
Open Workspace Folder \> Measurements\autosave\*.csv ****(see also
[\[1\]](#anchor-24)).

### <span id="anchor-25"></span>Zoom and Pan

The scope supports different zoom and pan operations.

****Important ****For zooming press **Shift** while defining the zoom
area with the mouse or rolling the mouse wheel.

For panning press **Ctrl** while dragging the scope area with the mouse.

Zooming or panning are only enabled when the scope is not running.

The zoom pull-down menu (Figure ) allows to set the desired zoom
behavior (horizontal/vertical/both) and provides additional commands
related to zooming:

-   <img
    src="gitbook/Pictures/Pictures/10000000000000AC000000EB0E11DBCFCF5DF3E9.png"
    title="fig:" style="width:4.551cm;height:6.218cm"
    alt=" Figure 14: Zoom menu items." />**Zoom to plots:** Sets the
    plot axes to the actual limit values of the curves.
-   **Zoom to cursors:** Restrict horizontal view to the range between
    the cursors (only available when both cursors are applied).
-   **Arrange Plots:** Automatically assign similar types of signals to
    one axis and arrange axes without overlap of the signals.
-   **Fix zoom range:** Set the default min/max range of the axes
    according the current zoom range.
-   **Undo zoom:** Undo the last zoom/pan operation.
-   **Reset zoom range:** Resets the min/max range to the default
    values.

### <span id="anchor-26"></span>Saving and Loading Scope Data

Use the ****Scope**** menu to save and load plot data (Figure ):

-   The scope data can be stored as a *\*.csv* file by using
    ****S****cope ****\>**** S****ave Plot Dat****a...****.
-   To open an existing data file in the scope, use ****S****cope ****\>
    ****Load Plot Data...****.
-   Further information about saving and loading plot data can be found
    in the application note about data exchange [\[1\]](#anchor-24).

Scope settings can be saved to avoid time consuming reconfiguration:

-   The plot settings, ranges, color and more, but without data, can be
    saved by executing Scope \> Save Configuration…
-   A saved configuration can be loaded by executing ****Scope
    ****\>**** Load**** Configuration…****. Already configured plots are
    not affected by loading a stored configuration.

To print or save an image of the scope including labels, use ****Scope
\> P****rint Plots****…****, ****Copy Image to Clipboard**** or ****Save
Plots as Image****…****. It is useful to customize the prints in advance
by changing properties of the ****Printing**** category in the ****Scope
****\> ****General**** tab.

### <img
src="gitbook/Pictures/Pictures/100000000000021F000002042E73AE3BB31F2EE7.png"
title="fig:" style="width:12.46cm;height:12.4cm"
alt="Figure 15: The Scope Menu The first section of the scope menu is related to zooming and panning. The next section is used to load and save plot data followed by an analysis section and a section to reset the scope. The last section handles the configuration of the scope." />Loading Templates

For each axis in the **Topology Tree**, the scope menu offers a ****Load
for \<axis name\>**** entry. When expanded, a number of templates are
available as shown in Figure . Each template will set up the scope for a
specific use with respect to the selected axis.

Several templates may be loaded in sequence for different axes. Use the
****Clear Scope**** menu to reset the scope to an initial state.

The first sub-menu entry ****F****r****om Configuration...****,****
allows to treat any previously saved scope configuration as a template
for the currently selected axis. This is manly used for configurations
where all plots refer to the same axis.

### <span id="anchor-27"></span>Analysis

The scope incorporates the most frequently used analysis functions.

As shown in Figure , the two cursors can be used to select and analyze
data. Each measure is shortly explained by its tool-tip. The first group
of measurements only examine the two points at the cursors, while the
second group considers all the data in the range defined by the two
cursors. A transparent shading is shown to indicate parts of the scope
**not** taken into account for calculations.

When the secondary cursor is inactive, the whole visible range is
considered for calculation.

Analysis also features an **FFT** calculation. When invoked, another
scope view is opened with the selected data plotted against the
frequency domain.

### <span id="anchor-28"></span>Formatting

The formatting and behavior of the scope, individual plots and cursors
can be configured in the respective tabs.

## <span id="anchor-29"></span>Triamec Workspace

When working with **TAM System Explorer**, different files are used or
generated e.g. configuration files, measurement data or firmware files.
The **Triamec Workspace** helps to manage and organize these files.
Basically the workspace is a directory where all files are stored in
dedicated folders. Using the workspace simplifies file handling, backup
and support. For different applications and machines it is recommended
to use separate workspaces.

The following table shows the structure of the workspace.

|           |               |                                                         |
|-----------|---------------|---------------------------------------------------------|
| 'WspName' | Configuration | TAM and scope configurations                            |
|           | Measurements  | Bode measurements, Plot data and pictures               |
|           | Firmware      | firmware files                                          |
|           | Tama          | Tama programs                                           |
|           | Projects      | Visual Studio projects, i.e. for creating Tama programs |
|           | Doc           | Documentation, readme, checklists                       |

A default workspace is generated when the **TAM *Software* is installed.
This default workspace folder is named ****Triamec**** and it is located
in the ****PublicDocuments ****folder. When **TAM System Explorer** is
started the first time, this workspace will be loaded. After a restart
of **TAM System Explorer**, the last used workspace will be loaded
automatically. Use the ****File**** menu to handle the different
workspaces:

-   ****File \> New \> Workspace****: creates a new workspace.
-   ****File \> Open Workspace****: loads an existing workspace.
-   ****File \> Open Workspace Folder****: opens the currently loaded
    workspace folder in Windows File Explorer.
-   ****File \> Recent Workspace \> ****…**** : select and load a
    recently opened workspace.

The currently active workspace folder is shown in the title bar of **TAM
System Explorer**.

## <span id="anchor-16"></span>TAM Configuration

The parametrization of a **Topology Tree** is called **TAM
Configuration**. The **TAM configuration** contains the parametrization
of the drives, the names of the nodes in the topology and other
information.

The **TAM Configuration** can be saved

-   **persistent on the drive:** If the **TAM Configuration** is saved
    persistent on the drive, this configuration becomes active directly
    after restarting the drive. A drive without a persistent **TAM
    Configuration** will load an initial configuration on start-up with
    default values for all registers.
-   or as a** \*.TAMcfg file on the PC:** The *\*.TAMcfg* file is useful
    to exchange a configuration between machines of the same type or to
    save and archive the configuration status of a machine. It is
    recommended to save the configuration during setup of the
    configuration occasionally to have a backup in case of a problem.  
    The *\*.TAMcfg* file is formatted as an **XML** file and can also be
    opened with a suitable editor (e.g. **Notepad++**) or with a file
    comparison tool to compare two different states of the configuration
    (**e.g. WinMerge**). Scope settings are *not* part of the **TAM
    **Topology Tree** and have to be stored separately (see section
    [3.3.7](#anchor-26)).

### <span id="anchor-30"></span>Saving the TAM Configuration Persistent on the Device

The following steps are required to save the **TAM Co**n**figuration**
persistent on the drive (see also Figure ):

1.  Right-click the station of the drive and select **Manage Persistence
    …**.
2.  Click **Save parameter permanently** to store the setting to the
    drive.

The **Manage Persistence …** dialog also allows to revert the current
configuration or to disable the persistence.

****Remark****s**** ****During the activation of the persistence it is
possible that the drive state changes to Unresponsive for a short
moment.

Persistence has to be set for each drive separately.

To reset the drive to default values, disable persistence and power
cycle the drive.

<figure>
<img
src="gitbook/Pictures/Pictures/1000000000000511000001D5A7270B745203C0E2.png"
style="width:15cm;height:5.424cm"
alt="Figure 17: Persistent TAM Configuration" />
<figcaption aria-hidden="true">Figure 17: Persistent TAM
Configuration</figcaption>
</figure>

### <span id="anchor-31"></span>Saving the TAM Configuration on a PC

To save the **TAM Configuration** on the PC the following steps are
required (see also Figure ):

1.  Open the save configuration dialog by clicking ****File \> Save TAM
    Configuration...****.
2.  The ****Include****s**** ****panel allows to select/unselect items,
    which should be stored with the **TAM Configuration**. It is
    recommended to use the default settings to save the configuration.

-   -   **Registers:** All parameter and information registers will be
        stored.
    -   **Tama assemblies:** If a **Tama** program is loaded to the
        drive either the path to the Tama program or the Tama code
        itself will be saved to the T**AM Configuration** (see also
        section [3.7](#anchor-32)).
    -   **Module assignments:** If a module is assigned to the
        **Topology Tree**, it will be saved to the **TAM
        Configuration**.
    -   **Module parameters:** Parameters related to the module will be
        saved.

1.  The ****Coverage**** panel allows to select which part of the
    **Topology Tree** should be saved:

-   -   If ****Starting f****ro****m topology**** root is checked
        (default), the whole **Topology Tree** with all devices assigned
        to it will be saved.
    -   If ****Starting from tam://...**** is checked, only items above
        the currently selected item in the **Topology Tree** will be
        saved. This is for example helpful, if only the configuration of
        a particular device should be saved.

1.  Clicking the ****Save**** button will open the ****Save As****
    dialog.
2.  After choosing a file name and clicking the ****Save**** button the
    progress window will pop up which shows the progress.
3.  <img
    src="gitbook/Pictures/Pictures/100000000000047B000002605DEAFFE08DCF9921.png"
    title="fig:" style="width:17.801cm;height:9.435cm"
    alt=" Figure 18: Save TAM Configuration on PC" />In case of an
    unexpected exception, the process may be started again by using the
    ****Restart**** button.

### <span id="anchor-33"></span>Load TAM Configuration

The following steps are required to load a **TAM Configuration**:

1.  Open the ****Load**** Configuration**** dialog by clicking ****File
    \> ****Load**** TAM Configuration...****.
2.  Select a matching ****TAM Configuration**** and click the
    ****Open**** button. A progress window will pop up.
3.  If issues are detected with the configuration, you will need to
    manually ****S****tart**** the process after having reviewed the
    warnings carefully ().
4.  In case of an unexpected exception, the process may be started again
    by using the ****Restart**** button.

<img
src="gitbook/Pictures/Pictures/10000001000004E8000002168C728D838ABA6EAE.png"
style="width:10.146cm;height:4.309cm" />

Figure 19: Configuration download progress window

When a **TAM Configuration** is loaded, the configuration is assigned to
the physically existing stations according to the following scheme:

-   If the name of a station in the tree does uniquely match with the
    name of a station in the configuration, the configuration of the
    station is assigned by name.

-   If the station name does not match or is not unique, and the serial
    number of the device does match, the configuration is assigned by
    serial number.

-   Stations that can't be assigned by name or serial number are
    assigned by station type, If a unique assignment according to the
    station type is possible,

-   If at this point there are still devices which are not assigned, the
    ****Resolve TAM configuration**** dialog is opened (Figure ).

    -   The dialog lists all stations available in the configuration at
        the left column of the table.
    -   With the pull down menu in the right column a (not jet assigned)
        station from the **T**AM T**opology Tree** can be assigned to
        the configuration.
    -   If the station does not exist in the current tree, select
        ****\<mark for removal\>****.
    -   To identify the target station, use the serial number or use the
        blink button. The blink button will cause a red blink of the
        axes **LED** and system status **LED**.
    -   Press ****Start**** in the ****Load configuration**** dialog to
        apply the assignment of the configuration.
    -   After a new assignment of the stations it is recommended to save
        the** TAM Configuration**.

<figure>
<img
src="gitbook/Pictures/Pictures/100000000000033E000001AAAC9F9D8934A75F45.png"
style="width:17.801cm;height:9.135cm"
alt=" Figure 20: Resolve configuration mismatch." />
<figcaption aria-hidden="true"><br />
Figure 20: Resolve configuration mismatch.</figcaption>
</figure>

### **Opening a TAM Configuration in Simulation Mode**

|                                                                                                                                                |     |                                                                                       |
|------------------------------------------------------------------------------------------------------------------------------------------------|-----|---------------------------------------------------------------------------------------|
| It is also possible to open a **TAM **C**onfiguration** file directly with the context menu of the *\*.TAMcfg* file (right click on the file): |     | <figure>                                                                              
                                                                                                                                                        <img                                                                                   
                                                                                                                                                        src="gitbook/Pictures/Pictures/1000000000000106000000944DFE537487FF83AF.png"           
                                                                                                                                                        style="width:5.001cm;height:2.82cm"                                                    
                                                                                                                                                        alt="Figure 21: Context menu of a TAM configuration file having extension .TAMcfg" />  
                                                                                                                                                        <figcaption aria-hidden="true">Figure 21: Context menu of a TAM                        
                                                                                                                                                        configuration file having extension .TAMcfg</figcaption>                               
                                                                                                                                                        </figure>                                                                              |

### Transferring a TAM Configuration 

It is often required to transfer a **TAM Configuration** from one
machine A (**MA**) to another machine B (**MB**) of the same type. This
can be done by executing the following steps:

1.  Give the stations of **MA** a meaningful name e.g. Station1_XY,
    Station2_ZB etc.
2.  Save the configuration of **MA** on the PC.
3.  Connect to **MB** and load the configuration.
4.  Solve the configuration mismatch by using the serial number or the
    blink button.
5.  Save the configuration for *MB* on the PC and persistent on the
    drive.

## <span id="anchor-34"></span>Updating Firmware

This section explains how to find a suitable firmware and how to
download the firmware to the device.

The newest firmware release can be downloaded from the **Triamec** web
page:

1.  Go to [www.triamec.com](http://www.triamec.com/) ****\>****
    ****Support**** ****\> ****TAM F****i****rmware****:****
2.  Open the web-page matching the product type of your device (e.g.
    ****\> TSD ****Series****). If the product type of your device is
    not known, you can identify it by clicking the station of the device
    in the **Topology Tree**. This opens the property page in the
    ****General**** tab as shown in Figure . You will find the type of
    the device under ****Product Information****. The property page also
    shows the currently installed firmware version and the product
    revision which could also be relevant for the selection of the
    firmware.
3.  Check the release notes for relevant changes of the firmware.
4.  Download the *\*.zip* file with the firmware package and unzip the
    file.

<img
src="gitbook/Pictures/Pictures/100000000000023C0000013D270BBEAF775E077F.png"
title="fig:" style="width:11.788cm;height:6.537cm"
alt="Figure 22: Station Properties. The product information shows the type, the product revision and the firmware version. " />Execute
the following steps to download the firmware:

-   Make sure that all axes are disabled and STO is not active.
-   Right click the device to open the context menu (Figure ).
-   From the context menu choose ****Update Firmware ****…****.
-   Select the desired firmware and click open. A filter assures, that
    only compatible files are selectable. If no firmware file is
    selectable, make sure you have downloaded the correct firmware
    package.
-   The ****Firmware File Download**** window pops up. Click
    ****Start**** to initiate the download. The green bar will show the
    progress of the download.
-   After the download succeeded, press ****Close**** to close the
    window.

<img
src="gitbook/Pictures/Pictures/10000000000001B0000000D9825F1F5776E84F6E.png"
title="fig:" style="width:10.673cm;height:5.376cm"
alt="Figure 23: Firmware download via the station node." />*Tria-Link*
adapters don't have a station node, they display the ****Update Firmware
****… ****context menu entry in their adapter node.

> ****Important ****If the replaced firmware version is older than 4.7
> or the **TAM System Explorer** version is older than 7.10 a power
> cycle of the drive is required to activate the new firmware!

> ****Warning ******S**afe Torque Off** must not be activated before and
> during a firmware download.

## <span id="anchor-32"></span><span id="anchor-20"></span>Working with Tama Programs

**Tama **p**rograms** are custom real time extensions to the device
firmware. They are written in C# and compiled to the proprietary *.tama*
assembly format, the **Tama **a**ssembly**. That said, both terms are
used interchangeably.

A Tama program has access to the complete register interface of a device
and consists of different tasks. The **isochronous** task runs in hard
real time while the **asynchronous** task runs within an interruptible
routine.

****Remark**** ****If you want to author a **Tama *p*rogram** yourself,
refer to the ****Tama Library**** sample (****Help \> Documentation \>
Software \> Samples****) or the related documentation
[\[5\]](#anchor-35) and [\[6\]](#anchor-36) (****Help \> Documentation
\> Software****).

### Enabling a Tama Program

<table>
<tbody>
<tr class="odd">
<td><p>For the handling of <em><em>Tama
</em><em>p</em><em>rograms</em></em> the
<em><em>Tama </em><em>M</em><em>anager</em></em> is used. The
<em><em>Tama Manager</em></em> is located below the device node in the
<em><em>TAM Topology Tree</em></em>.</p>
<p>The following steps are needed to run a <em><em>Tama
</em><em>p</em><em>rogram</em></em> on a device:</p>
<p>To remove the <em><em>Tama </em>p<em>rogram</em></em> from the
device, use the <strong><strong>Dismiss Tama assembly</strong></strong>
menu item.</p>
<p>An assigned<em><em> Tama </em>p<em>rogram</em></em> can be downloaded
from the drive to the computer by clicking <strong><strong>Download
</strong><strong>Tama </strong>a<strong>ssembly</strong><strong>...
</strong></strong>in the context menu.</p></td>
<td><img
src="gitbook/Pictures/Pictures/10000000000001A90000016801E9EBA773C7E1A7.png"
title="fig:" style="width:8.047cm;height:6.814cm"
alt="Figure 24: Context Menu of the Tama Manager. The menu entries also indicate whether the virtual machines are currently enabled or not." /></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><img
src="gitbook/Pictures/Pictures/100000000000022A0000014E779F554B5830AA31.png"
title="fig:" style="width:14.66cm;height:8.839cm"
alt="Figure 25: Tama assembly download dialog containing helpful information" /></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

> ****Warning ****A running **Tama** *p*rogram** can strongly influence
> the behavior of a device. In case of unexpected behavior, first check
> if a **Tama** *p*rogram** is enabled and consider disabling it.

### Tama Control

The following items are provided to control the execution of the **Tama
*p*rogram**.

-   Registers Application.TamaControl can be used to monitor the state
    of the **Tama vir**t**ual machine** and also to interact with the
    **Tama *p*rogram** (depending on the implementation).
-   The axis monitor displays the state of the **Tama virt**u**al
    machine** (see section [3.2](#anchor-18)).
-   The icons of the entries in the context menu of the** Tama Manager**
    also indicate whether the **VM** is enabled or disabled.

### <span id="anchor-37"></span>Saving** a **Tama Program **P**ersistent on the Device

The currently loaded **Tama *p*rogram** can be saved persistent together
with the **TAM Configuration** as described in section
[3.5.1](#anchor-30)**.**

****Remark**** ****When a persisted **Tama *p*rogram** is replaced with
a new **Tama *p*rogram**, the steps described in section
[3.5.1](#anchor-30) have to be executed again, to persist the new **Tama
*p*rogram**.

A persisted **Tama *p*rogram** will automatically be loaded after a
restart of the device but remains disabled after restart by default. To
automatically enable a **Tama *p*rogram** at start-up set the register
General.Parameters.EnableAsynchronousTama or
General.Parameters.EnableIsochronousTama to TRUE.

### Saving a Tama Program in **a** **TAM** Configuration File

When the configuration is saved (see section [3.5.2](#anchor-31)) while
a **Tama *p*rogram** is loaded, the assembly is also saved to the
configuration by default.

## <span id="anchor-38"></span>Global Keys

The following keys are always active when TAM System Explorer is active.

**Key** **Effect**

**F5** Start/Stop Scope

**F12** Emergency switch off all power sections. You may also click the
button located on the left of the axis monitor.

****Caution**** ****Switching off the power section of a drive during
motion may damage the axis.

*Pause/Break* Emergency Stop of all active axes. You may also click the
button located on the left of the axis monitor.

# <span id="anchor-4"></span>Plug-In Modules

The whole functionality of a **Triamec** device can be accessed directly
by interacting with the registers of **Topology Tree**. However, this
can be rather extensive and complicated. To simplify dedicated tasks,
plug-in modules can be assigned to the **Topology Tree**. These modules
provide a graphical user interface which allows to interact with the
device while reading and writing of the registers is handled by the
module.

<figure>
<img
src="gitbook/Pictures/Pictures/100000000000050D0000013B4D83A3A19F1ABDB3.png"
style="width:17.801cm;height:4.336cm"
alt=" Figure 26: Axis module assignment." />
<figcaption aria-hidden="true"><br />
Figure 26: Axis module assignment.</figcaption>
</figure>

With the following steps, an ****Axis**** or ****AxisGroup ****module
can be assigned to a device (Figure ):

1.  Right click the device to open the context menu of the device.
2.  Click ****Assign module…****
3.  The module is assigned to the **Topology Tree**. To access sub
    modules, unfold the module node in the **Topology Tree**. The user
    interface is shown in the tab panel in ****Module \> View****.
    Parameters assigned to the module are shown in ****Module \>
    Parameter****.

To remove a plug-in module open the context menu of the module, then
click ****Remove module****.

## <span id="anchor-19"></span>Axis Module

<img
src="gitbook/Pictures/Pictures/10000000000000B60000006F76D7FE5F3FBE568D.png"
title="fig:" style="width:4.815cm;height:2.937cm"
alt=" Figure 27: Unfolded Axis Group" />The axis module can be used to
execute basic movements of the axis. For dual-axis drives an ****Axis
Group****-module should be added to the **Topology Tree**. Unfold the
module-node and select the desired axis. The user interface of the axis
is then shown in the tab panel in ****Module \> View ****(Figure ). If
the ****Axis**** node is expanded further, additional tools like **Bode
Tuning** are accessible.

<img
src="gitbook/Pictures/Pictures/2000011800004A3800002450B400FF21821E0D1C.svm"
title="fig:" style="width:15.813cm;height:7.781cm" />The axis module
offers the following controls to interact with the axis (see also Figure
):

1.  **Attach/**Detach****: In case the **Attach** button is shown, this
    button needs to be pressed in order to enable the controls of the
    module. This button prohibits commands from the superior control
    system (e.g., EtherCAT) to allow the module to control the axis.
    Pressing the button sets
    Axes\[0\].Commands.General.OverrideControlSystem to 1. Release the
    button (**Detach**) to return control to the superior control
    system. If the button is not shown, no action is needed[^2].
2.  **Reset**: The ****Reset**** button can be used to reset pending
    errors or warnings. If the reset was successful, the drive returns
    to the Disabled state. If the reset was not successful, additional
    actions are needed by the user depending on the type of the
    error/warning.
3.  **Enable**/****Disable****: This button is used to enable or disable
    the axis. After the axis is successfully enabled, the axis state is
    Standstill. If ****Disable**** is pressed, the axis-state will
    change to ReadyToSwitchOn or Disabled.
4.  Status indicator.
5.  At the top right corner the following information is displayed:

-   -   The axis name (Axes\[\].Information.AxisName)
    -   The axis state (Axes\[\].Signals.General.AxisState)
    -   The actual position
        (Axes\[\].Commands.PositionController.MasterPosition)

1.  **Move to ***A*****: Pressing this button causes the axis to move to
    the position specified in field ****A****. Use the corresponding
    ****M****-button to load the actual position to field ****A****.
2.  ****Move A*****B*****: Pressing this button causes the axis to move
    towards position ****A**** and then to position ****B****. Use the
    corresponding ****M****-button to load the actual position to fields
    ****A**** or ****B. ****If the axis is already located at A, only a
    move to B is executed. If the ****Loop After****-checkbox is
    checked, the move sequence A B will be repeated until another move
    button or the stop button  is pressed. The wait time field at the
    right is used to set the delay at A and B before the next move
    starts.
3.  **Couple**: This button can be used to couple the axis to an
    internal or external trajectory generator (e.g. master slave mode or
    trajectory generation by a **Tama *p*rogram**). See also the related
    documentation [\[7\]](#anchor-39). Use the stop button  to
    decouple.
4.  Jog and Stop buttons:

-   -   Press the stop button  to terminate an ongoing move.
    -   Continuous jog negative  / positive : Pressing this button
        starts a continuous move. The move will run until another move
        button or the stop button  is pressed.
    -   Jog negative  / positive : While pressing this button the axis
        moves in the desired direction. The move will stop when the
        button is released.

1.  ****Dynamics****: These two fields can be used to reduce the
    dynamics of the move.

-   -   ****Vel.****: This field specifies the velocity used for the
        move relative to
        Axes\[\].Parameters.PathPlanner.VelocityMaximum.
    -   ****Acc.****: This field specifies the acceleration used for the
        move relative to
        Axes\[\].Parameters.PathPlanner.AccelerationMaximum.

1.  ****Set Position****: Pressing ****Set Position**** sets the actual
    position to the value specified in field S.

****Important**** ****If the ****Activation**** panel shows an
****Attach**** button, this button needs to be pressed in order to
enable the controls of the module. Release the button (****Detach****)
to return control to the superior control system.

Sub-Modules

-   ****Coupling Manager****: This module can be used to setup the
    coupling of the axis to an internal or external trajectory generator
    (e.g. master slave mode or trajectory generation by a **Tama
    *p*rogram**). See also the related documentation
    [\[7\]](#anchor-39).
-   ****Bode Tuning****: See chapter [4.2](#anchor-40) **Bode
    Analysis**.

## <span id="anchor-40"></span>Bode **Tuning**

The ****Bode ****Tuning ****module is used to measure the dynamic
characteristic of an axis in frequency domain and to tune the controller
based on this measurement. The following sections describe the steps
required.

Find the ****Bode Tuning**** module in the ****Axis Group**** module****
****and open the ****View**** ****tab. ****T****he ****View**** ****tab
****contains ****the following buttons:

-   ****Do a Bode Measurement...**** ****opens the ****Bode
    Measurement**** application. The application allows to configure and
    to execute the measurement.
-   ****Open Bode Measurement...**** opens a **Bode** measurement in the
    ****Bode ****T****uning**** editor. The editor allows to modify the
    controller parameter and directly visualizes the effect of the
    modification on the Bode plot.

<figure>
<img
src="gitbook/Pictures/Pictures/100000010000048F00000115A2AD6B64A37BCAAE.png"
style="width:15.333cm;height:3.641cm" />
</figure>

## <span id="anchor-41"></span>Bode Measurement

The Bode measurement allows to acquire the frequency response of the
axis. This measurement is required for **B**ode** tuning and therefore
has to be executed first.

### <span id="anchor-42"></span>Preparation:

****Warning**** The **Bode** measurement causes the axis to move.
Therefore a safe environment and setup is required and the drive has to
be configured correctly.

The following parameters must be set correctly. An incorrect
parametrization could influence the measurement results or damage the
motor. See also section [5.2](#anchor-43) on how to configure these
parameters.

-   Axes\[\].Parameters.Motor.Type
-   Axes\[\].Parameters.Motor.InvertDirection
-   Axes\[\].Parameters.Motor.PolePairs
-   Axes\[\].Parameters.Motor.EncoderCountsPerMotorRevolution
-   Axes\[\].Parameters.Motor.PeakCurrent
-   Axes\[\].Parameters.Motor.NominalCurrent
-   Axes\[\].Parameters.PositionController.Encoders\[\].Type
-   Axes\[\].Parameters.PositionController.Encoders\[\].InvertDirection
-   Axes\[\].Parameters.PositionController.Encoders\[\].Pitch
-   Axes\[\].Parameters.PositionController.OutputLimit
-   Axes\[\].Parameters.Commutation. *…*
-   Axes\[\].Parameters.CurrentController.OutputLimit
-   
-   General.Parameters.EncoderTopology
-   General.Parameters.DcBusVoltageUpperLimit
-   General.Parameters.DcBusVoltageLowerLimit

****Important**** Make sure that the axis is moving freely during the
measurement. If the axis is touching an obstacle or an end stop, the
measurement will not reflect the correct behavior of the axis.

To avoid moving against an end stop e.g. if the direction of the axis is
vertical, a soft material like foamed plastic can be used to underlay
the axis. If the axis is equipped with a brake, the brake has to be
released during the measurement. In case of air bearings the correct air
pressure must be applied.

### Measurement Setup

<img
src="gitbook/Pictures/Pictures/10000001000006240000048C4C32383AA387BEE0.png"
title="fig:" style="width:17.801cm;height:13.044cm" />To start the
measurement click the ****Measure ****Bode ****Plot…**** button (Figure
). This opens the window with the application as shown in Figure .

The following parameters can be set:

-   ****Min Frequency****: This parameter defines the lower limit of the
    frequency range used for the measurement (default 20Hz).
-   ****Max Frequency****: This parameter defines the upper limit of the
    frequency range (default 10kHz).****
-   ****Frequency Steps****: This parameter defines the resolution of
    the measurement in the frequency range. Depending on the 'Spacing'
    parameter the range defined by 'Min Frequency' and 'Max Frequency is
    divided logarithmically or linearly into the number of 'Frequency
    Steps'. With a higher number of frequency steps, the measurement
    takes longer but will provide a higher resolution which is
    especially crucial to capture sharp resonances (default 300 Steps).
-   ****Wait Before Acquire****: This parameter defines the wait time
    between the start of the harmonic excitement to the start of the
    acquisition (default 0.1s).
-   ****Output Maximum****: This parameter defines the maximum allowed
    amplitude of the voltage signal. The default value is half of the
    output limit according register
    Axes\[\].Parameters.CurrentController.OutputLimit.
-   ****ActualCurrentQ Maximum****: This parameter defines the maximum
    allowed amplitude of the current. The default value is half of the
    nominal current of the motor according register
    Axes\[\].Parameters.Motor.NominalCurrent. The value is limited by
    Axes\[\].Parameters.PositionController.OutputLimit
-   ****Position Maximum****: This parameter defines the maximum allowed
    amplitude of the position. The default value is 20 times the encoder
    pitch according register
    Axes\[\].Parameters.PositionController­.Encoders\[\].Pitch.
-   ****Spacing****: Defines if the range between ****Min Frequency
    ****and ****Max Frequency ****is sampled ****L****ogarithmic****ally
    or ****L****inear****ly (default ****L****ogarithmic****).
-   ****Method****: ****Open Loop Bode**** or ****Closed Loop Bode****
    can be selected. ****Closed Loop Bode**** requires a stable setting
    for the position controller and the current controller (default
    ****Open Loop Bode****).

****Warning**** The three parameters ****Output Maximum****,
****ActualCurrentQ Maximum**** and ****Position Maximum**** are used to
deduce the amplitude of the harmonic excitation of the axis. This
parameters must be set with caution, as too big an excitation can damage
the axis. It is recommended to start with small values for the
amplitudes (especially for ****ActualCurrentQ Maximum****) and to
increase the values carefully until a sufficient signal to noise ratio
is reached.

A Bode measurement can generate loud noise also in frequencies that are
not perceived by the human ear. Wear hearing protection and keep animal
companions away.

### Measurement

The following controls are available for the execution of the
measurement:

-   ****Start****: When the 'Start' button is pressed, the measurement
    starts.
-   ****Stop****: The measurement can be aborted with the 'Stop' button.
-   ****E****xit****: Close the Bode measurement window.

Start the measurement by pressing ****Start****. During the measurement
the amplitude of the output signal is adapted in such a way that
amplitudes of the states (voltage, current and position) are as big as
possible but do not exceed the specified maximum.

<img
src="gitbook/Pictures/Pictures/10000000000002BD000001A7525DAC41BCC2E20A.png"
title="fig:" style="width:13.527cm;height:8.16cm"
alt="Figure 31: Bode measurement result." />Once the measurement is
done, the ****Bode Measurement Result**** window is opened (Figure )
which allows to examine the quality of the signals.

To use the measurement with the Bode Tuning tool, the measurement has to
be saved by clicking the**** Save ****button. The measurements are saved
in a *\*.csv* file.

### Remarks

For a first recording it is recommended to use the following frequencies
settings:

-    ****Max Frequency**** = 24000 Hz; ****M****in**** Frequency**** =
    20 Hz; ****Frequency Steps**** ≥ 300

In some cases it is required to have a higher resolution in the
frequency domain, for example for axes with critical resonances. In this
case, to have a good resolution at higher frequencies but also do the
measurement in reasonable time it is recommended to do the measurement
in two sessions:

-   Session 1: ****Max Frequency**** = 24000 Hz; ****M****in****
    Frequency**** = 200 Hz; ****Frequency Steps**** ≥ 500
-   Session 2: ****Max Frequency**** = 200 Hz; ****M****in****
    Frequency**** = 20 Hz; ****Frequency Steps**** = 200

The dynamic behavior of a machine may change depending on the location
of the axes. Therefore it is recommended to do the measurement at
several locations in the machine workspace.

Generally the quality of the measurement increases with bigger
amplitudes (especially with low resolution encoders or high friction),
but the restrictions of the machine must be considered when increasing
the maximum values.

Normally, the phase plot of response **X/I** should show a phase shift
of about 180° at low frequencies. If the phase shift is closer to 0°,
the parameter Axes\[\].Parameters.Motor.InvertDirection might have to be
altered (see also section [5.5.1](#anchor-44)).

If the excitement of the axis varies depending on the position of the
motor probably one of the following parameters is not set correctly:

-   Axes\[\].Parameters.Motor.InvertDirection
-   Axes\[\].Parameters.Motor.PolePairs
-   Axes\[\].Parameters.Motor.EncoderCountsPerMotorRevolution

In some cases it is required to do a closed loop measurement e.g. to
avoid drifting of the axis. In this case the ****Method**** property can
be set to ****Closed Loop Bode****. A closed loop bode measurement
requires stable parametrization of the position controller.

When two encoders are configured for the axis (e.g. dual-loop), the
signals from both encoders will be acquired.

It is possible to further customize the **Bode** measurement. For
example to measure cross coupling between two axis or to measure a
signal from an external sensor read by an option module. See ****Help \>
Developer Samples \> *****SWNET_TamSoftwareSamples\*/BodeConfig* for
more information.

## <span id="anchor-45"></span>**Controller** Tuning

The saved Bode measurements can be used to design and optimize the
position and current controllers with the ****Bode Tuning**** editor.
The following steps are required to open the saved **B**ode**
measurements in the editor:

-   To open measurements in the editor click ****Tune Controllers…****
    (figure ).
-   Select one or several measurements and click 'Open'. Use **Ctrl** or
    **Shift** to select more than one file. Make sure the measurement
    corresponds to the selected axis in the **Topology Tree**.
-   The ****Bode Tuning**** editor is opened and the frequency response
    of the current loop is displayed[^3].

### Editor Window

<img
src="gitbook/Pictures/Pictures/1000000100000554000004D1106182CF15CD20A1.png"
title="fig:" style="width:17.801cm;height:16.071cm"
alt=" Figure 32: Bode Tuning editor with current controller and Bode plot selected." />The
editor consists of the following items (see also figure ):

1.  ****Title Bar****: In the title bar, the name of the selected axis
    is shown. Make sure the axis is consistent with the loaded
    measurements.
2.  ****Select Controller****: This radio button can be used to switch
    between different controllers e.g. current loop or position loop.
3.  ****Control Parameter****s****: The parameters of the selected
    controller loop are displayed and can be modified. If a parameter is
    modified, the values are stored like prepare values in registers:
    The background changes its color to orange, indicating a modified
    but not yet committed parameter. After each change, the **Bode** and
    **Nyquist** Figures are recalculated. When some parameters are
    illegal, no data is drawn.
4.  ****Commit Parameters****, ****Revert****, ****Compare****:

-   -   ****Commit Parameters****: Modification of parameters does not
        affect the configuration of the drive. Only when the commit
        button is pressed, the drive configuration will be updated with
        the modified values.
    -   ****Revert****: This button is used to reset the parameters to
        the actual drive-configuration.
    -   ****Compare****: Press and hold this button to show the transfer
        functions of the actual drive-configuration. This can be used to
        compare modified parameters with the actual drive setup.

1.  **View**: ****Reset Zoom**** can be used to reset zoom and pan
    operations.  
    Checking ****Wrap Phase**** reduces the phase range into \[-360,0\]°
    in the Bode plot. It has no effect in the Nyquist plot.
2.  ****Bode ****/**** Nyquist****: In the top right corner, the display
    mode of the frequency response can be selected:

-   -   ****Bode****: The amplitude response and the phase response of
        the axis are plotted. The signal colors match to transfer
        functions as following (see also figure ).

        -   Red: calculated open loop frequency response based on the
            measurement and the controller parameters
        -   Blue: controller transfer function
        -   Green: calculated closed loop frequency response based on
            the measurement and the controller parameters

    -   <img
        src="gitbook/Pictures/Pictures/10000001000003E8000000E98E24322844B1A338.png"
        title="fig:" style="width:11.684cm;height:2.722cm"
        alt="Figure 33: Signal colors according to transfer functions in the control loop." />****Nyquist****:
        The red curve shows the open loop frequency response in the
        complex plane calculated based on the measurement and the
        controller parameters.

1.  ****Cursor****: A cursor is shown together with a label at the top
    left corner of the graph. The label displays the frequency, gain and
    phase at the cross-hair location. To select a different signal, the
    cross-hair has to be dragged to the new signal. At the beginning,
    the cursor might be hidden at the boundaries of the graph.
2.  <img
    src="gitbook/Pictures/Pictures/10000000000001D500000071C9A208E68806251D.png"
    title="fig:" style="width:12.383cm;height:2.99cm"
    alt="Figure 34: When opening Bode measurements, you can choose whether to append new data, or to replace all measurements currently shown in the Bode tuning window." />****Legend****:
    The first three legend items show the colors for controller
    (**Gr**), closed (**Gclosed**) and open (**Gopen**) loop curves. For
    each loaded measurement, a legend item is generated, showing the
    file name and the curve colors. Hovering over the legend items will
    highlight **G**open** and **G**closed** loop curves from the
    respective measurement. If many files are loaded, the legend will
    wrap. In this case the size of the legend frame may be adjusted by
    dragging the upper border or the vertical scroll-bar at the right
    can be used.  
    You can add and remove measurements via the legend.  
    Remove a measurement by clicking on the ****X**** button which fades
    in when hovering over the legend item.  
    Add measurements using the ****+**** button on the right side of the
    legend. In the ****Open Bode **Plot(s)** dialog set the radio button
    either to ****Append**** in order to add the measurement to the
    loaded measurements, or ****Replace**** to only load the new
    measurement (figure ). The same dialog is shown when repeatedly
    using the **T**une Controllers…**** ****button in the
    ****Modul****e**** View**** tab.

### Zooming and Panning

This section describes how to zoom and pan the plot area:

-   Press *Shift* and left mouse-key while defining the zoom area with
    the mouse.
-   Press *Ctrl* and left mouse-key to pan the plot area.
-   To undo the zoom area: press *Shift* or *Ctrl* and right mouse-key
    to reset the zoom area.
-   Zooming is also possible by pressing *Shift* and turning the
    mouse-wheel.
-   If zoom is applied, the cross-hair can be out of scope. Zoom out is
    required (e.g. *Shift* + scroll wheel).
-   Reset zoom using the respective button.

# <span id="anchor-5"></span>Drive Configuration

This chapter explains how to configure the registers in the Topology
Tree to commission a servo axis. The commissioning steps are also
visualized in chapter [8](#anchor-46).

## <span id="anchor-47"></span>Preparation

If the servo drive was already used for a different setup it is
recommended to reset it to default settings right-clicking the device
node in the register tree, then clicking – ****Manage
****persistence.****..**** – ****Disable ****persistence**** and
rebooting the drive.

### Required Data

Before commissioning a servo axis, axis specifications are needed. This
section gives an overview of the required data. If desired, additional
values can be written to the Axes\[\].Information registers (see also
section [3.1.4](#anchor-17)).

##### Motor

Specifications found in the motor data sheet:

-   Type of motor: dc/ac, synchronous, linear/rotational

-   Peak current[^4]

-   Nominal current

-   Thermal time constant or current square time constant (or peak
    current duration)

-   if rotational motor

    -   Torque constant
    -   Number of pole pairs (check if number of pole pairs or if number
        of poles is specified)
    -   Screw pitch if axis with lead screw

-   if linear motor

    -   Force constant
    -   Pole-pair pitch (distance between two north-poles or two
        south-poles)

-   if motor temperature is observed by the drive:

    -   Type of sensor
    -   Temperature limit

##### Encoder

Specifications found in the encoder data sheet:

-   Encoder pitch or encoder counts per motor revolution
-   Max allowed encoder speed

##### Additional information about the axis

The following aspects of the axis should be considered before
commissioning an axis:

-   How should the axis be named (e.g. Axis_X, Axis_Y ...)
-   Total inertia of the axis
-   Topology of the axis (linear/rotational, single-loop/dual-loop,
    horizontal/vertical, ...)
-   How are the encoders connected to the drive (which connector of the
    drive is used to connect the encoders)
-   How is the motor connected to the drive (which connector of the
    drive is used to connect the motor)
-   How will the axis be referenced
-   Move range of the axis
-   Dynamic specifications of the axis (max velocity, max acceleration,
    max jerk)
-   How should the axis be controlled (**TwinCAT**, stand-alone with
    **Tama** program, **PC**-application with **TAM *API*)
-   Safety considerations (**STO**, ...)
-   Additional requirements …

### <span id="anchor-48"></span>Naming of Stations and Axes

<img
src="gitbook/Pictures/Pictures/100000000000010C000000F547422E1FF2E4AAEE.png"
title="fig:" style="width:6.001cm;height:5.241cm"
alt=" Figure 35: Example for renaming of stations and axes." />To easily
identify the related physical axis, it is recommended to change the
station name and the axis name to a meaningful expression. For example
if Axis0 is used to drive the **X** axis and Axis1 is used to drive the
**Y** axis, name the station **Station_XY** and the axes **Axis_X** and
**Axis_Y**. See sections [3.1](#anchor-14) and [3.2](#anchor-18) for how
to rename stations and axes.

### Units

The unit for the position can be set with register
Axes\[\].Parameters.PositionController.PositionUnit. For linear axes
**m** or **mm** and for rotational axes **turns**, **degree** or **rad
**can be set.

****Not****e**** ****It is recommended to set the unit for the position
prior to commissioning the drive. All other dimensions are defined
according the** International System of Units (SI)**.

## <span id="anchor-43"></span>Initial Setup of the Register Tree

This section describes the initial setup of the parameter registers. It
is good practice to fill the registers from top of the tree to bottom
while leaving not yet known parameters (e.g. controller gains) out for
later configuration. This section follows this practice and explains how
to set the relevant parameters for a common application. Parameters not
covered in this section keep their default value. See section
[3.1.1](#anchor-15) on how to write and commit parameters. For people
with experience in Triamec drive configuration, can lead you through the
setup.

****Rema****rk**** ****If the drive was used for a different application
before, it is recommended to reset the registers to default values (see
section [3.5.1](#anchor-30)).

The register Tree contains three nodes:

-   **General:** The General node contains registers which are relevant
    for the drive but not dedicated to an axis.
-   **Axis:** The Axis node contains registers which are related to the
    axis.
-   ****Application****: These registers are only relevant in
    conjunction with a **Tama *p*rogram** and are not covered in this
    section.

The following parameters must be configured for an initial setup:

### General.Parameters

-   DcBusVoltagelowerLimit, DcBusVoltageUpperLimit: This values are used
    to monitor the DC bus voltage (General.Signals.DcBusVoltage). If the
    measured DC bus voltage is out of the specified range, a
    DcBusVoltageOutOfRange error is issued.  
    It is recommended to set the range plus minus 10 to 20 % of the
    nominal DC bus voltage. For applications with recuperation of energy
    (e.g. spindles) the upper limit has to be set slightly above the
    setpoint voltage of the brake resistor. The setpoint of the brake
    resistor can be found in the hardware manual of the power supply.
-   EncoderTopology: The EncoderTopology is only different from Standard
    if the encoders are connected to the drive in a nonstandard way e.g.
    if option modules are used (see also [\[8\]](#anchor-49)).

### <span id="anchor-50"></span>Axis\[\].Parameters.Motor

This node contains registers related to the motor.

-   Type: Servo axes mostly use three-phase synchronous motors for both
    linear and rotational axes. Set Type to SynchronousAC in this
    case.  
    In case of a DC-motor (e.g. brushed dc-motors, voice-coil motor...)
    set Type to DC.

-   BrakeReleaseAction: This parameter allows to select a digital output
    which is set to release the brake when the axis is enabled.

    -   With 'SetOut1' the digital output O1 is set. Also the Brake
        output of the motor connector X40 is set.
    -   With 'SetOut2' the digital output O2 is set.
    -   For more information of how to connect the brake see the
        corresponding hardware manual.

-   <img
    src="gitbook/Pictures/Pictures/1000000000000514000002EB3117ED251E92BFC7.png"
    title="fig:" style="width:13cm;height:7.47cm"
    alt=" Figure 36: BrakeHoldTime: Timing diagram of the brake output with BrakeReleaseAction = SetOut1 and BrakeHoldTime = 1s." />BrakeHoldTime:
    If there is a significant delay between the instance when the brake
    output is reset and the instance when brake is applied mechanically,
    the BrakeHoldTime can be used to compensate this delay. The axis
    will remain enabled for the duration of BrakeHoldTime to avoid a
    movement of the axis during this delay.  

-   InvertDirection: With this parameter it is possible to alter the
    electrical direction of the motor.  
    The position controller prerequisites, that the electrical direction
    of the motor has the same orientation as the direction of the
    encoder. If the orientation is opposite, the parameter
    InvertDirection has to be altered to align the directions. If the
    encoder direction is changed, flip the motor InvertDirection too.  
    An incorrect setting of this parameter is often the cause for
    problems when the motor is enabled the first time. The following
    symptoms could indicate an incorrect setting which requires to alter
    the parameter InvertDirection:[^5]

    -   The **B*ode* measurement shows a phase shift of about 0° or a
        multiple of 360°. A phase shift of -180° is expected if the
        alignment is correct.
    -   For a 3-phase motor, if the excitement of the axis varies
        depending on the position of the motor during the **B**ode**
        measurement.
    -   The enabling fails immediately after the phasing of the axis.
    -   If a current causes the axis to move in opposite direction.

-   PolePairs: This value has to be set to the number of pole pairs
    according to the data-sheet of the motor. In case of a **linear
    motor** or a **DC-motor**, this value is set to 1.

-   EncoderCountsPerMotorRevolution: This parameter describes the number
    of encoder lines per motor revolution. The definition of this
    parameter depends on the type of motor (linear/rotational) and the
    type of encoder (absolute/relative). See also [\[8\]](#anchor-49)
    for more information.

    -   In case of a rotational motor and a relative or analog
        encoder[^6], EncoderCountsPerMotorRevolution corresponds to the
        number of encoder lines per motor revolution.
    -   In case of a rotational motor and an absolute encoder without
        analog signals[^7], set EncoderCountsPerMotorRevolution to 1.
    -   In case of a linear motor, set this parameter to the number of
        encoder lines per pole pair pitch:  
        EncoderCountsPerMotorRevolution = **PolePairPitch** /
        **EncoderPitch**. The value for the **PolePairPitch** can be
        taken from the motor data sheet. The value for **EncoderPitch**
        is taken from the encoder data sheet (see also ).

-   PeakCurrent: This parameter has to be set to the peak current
    specified in the data sheet of the motor. If the absolute current
    applied to the motor exceeds the value of PeakCurrent a
    MotorPeakCurrentLimit error is issued.  
    For three-phase motors, consider if the current is given as peak
    value or as root mean square value (RMS). If the value is specified
    as root mean square, multiply it by .

-   NominalCurrent: This parameter has to be set to the nominal current
    specified in the data sheet of the motor. If the averaged current of
    one of the motor phases exceeds this value, a MotorI2t error is
    issued.  
    For three-phase motors, the value has to be entered as root mean
    square value (RMS) which is also the scale used in most data sheets.

-   
    $$\mathit{CurrentSqareTime} = \frac{- \mathit{PeakCurrentDuration}}{\ln\left( {1 - \frac{2 \cdot \mathit{NominalCurrent}^{2}}{\mathit{PeakCurrent}^{2}}} \right)}$$
    CurrentSquareTime: This parameter is used for the calculation of the
    i2t current and corresponds to to the **Thermal Time Constant **of
    the motor. The **Thermal Time Constant **should be specified in the
    motor data sheet. If the **Thermal Time Constant **is not available
    but the **Peak Current Duration** is specified, the
    CurrentSquareTime** **can be calculated with the following equation:

    If both values aren't specified, set this value to 10-30s for an
    iron-less motor and 60-600s for an iron-core motor.

****Warni****ng**** ****The limitation of the current (NominalCurrent,
PeakCurrent, CurrentSquareTime) must be configured correctly before the
drive is enabled the first time. Incorrect settings could damage the
motor.

### <span id="anchor-51"></span>Axis\[\].Parameters.PathPlanner

This node contains the parameters relevant for the internal path
planner. These parameters do not influence the trajectory generation of
an external control system like **Twin**CAT**. Nevertheless, the
parameters need to be set to reasonable values as the internal path
planner is used for testing of the controller loop and also for some
moves commanded by the external control system (e.g. homing moves).
Moreover the setup of the modulo values need to be in accordance with
the setup of the external control system (e.g. TwinCAT).

-   ModuloPositionMaximum and ModuloPositionMinimum: If the axis does
    not require a modulo motion, which is the normal case if an axis is
    not a spindle, both values are set to zero. Modulo motion is
    typically required for spindles with long running velocity moves and
    without a restriction of the move range. For example a typical
    setting for the modulo range with position unit in radian is:

    -   ModuloPositionMaximum = 6.283185307179586476925286766559 (= 2π)
    -   ModuloPositionMinimum = 0.0

The dynamic settings of the path planner depends on the mechanical and
electrical properties of the axis and on the requirements of the
process. The following inequations may help to estimate reasonable upper
limits for the settings:

|                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                         
 $$\begin{matrix}                                                                                                                         
 {{u\_{\mathit{\max}} \> \frac{JL}{K\_{t}}}{r\_{\mathit{\max}} + \frac{JR}{K\_{t}}}{a\_{\mathit{\max}} + K\_{v}}v\_{\mathit{\max}}} \\\\  
 {{i\_{\mathit{\max}} \> \frac{J}{K\_{t}}}{a\_{\mathit{\max}} + T\_{\mathit{ext}}}} \\\\                                                  
 \end{matrix}$$                                                                                                                           |

Maximal velocity **v*<sub>*max*</sub>* \[rad/s\] Inductance of the motor
**L** \[H\]

Maximal acceleration **a*<sub>*max*</sub>* \[rad/s<sup>2</sup>\] Inertia
of the rotor **J** \[kg m<sup>2</sup>\]

Maximal jerk **r*<sub>*max*</sub>* \[rad/s<sup>3</sup>\] Induced voltage
constant **K*<sub>*v*</sub>* \[Vs/rad\]

Maximal current **i*<sub>*max*</sub>* \[A\] Moment-current constant
**K*<sub>*t*</sub>* \[Nm/A\]

Maximal voltage **u*<sub>*max*</sub>* \[V\] External torque
**T*<sub>*ext*</sub>* \[Nm\]

Resistance of the motor **R** \[W\]  

For DC motors the maximal voltage is given by the DC bus voltage and for
AC motors by the DC bus voltage divided by square root of three. The
inequations above are simplified.

-   PositionMaximum and PositionMinimum: Set soft limits for the stroke
    of the axis. If the axis does not require soft limits, both values
    are set to zero. Values other than zero enable the following
    behavior.

    -   If a move command such as **MoveAbsolute** targets a position
        outside the limits, the move is rejected with an error message.

    -   If the axis is in coupled motion and the control system runs out
        of limit, the axis will throw an error at the soft limit
        position and trigger an emergency stop.

    -   If the axis already is outside the limits, only move commands
        towards the legal side are allowed. The same applies to coupled
        motion, with the following restrictions.

        -   If the position is higher than PositionMaximum, the velocity
            must be negative[^8].
        -   If the position is smaller than PositionMinimum, the
            velocity must be positive.  

-   VelocityMaximum: This parameter specifies the max allowed velocity.
    The following aspects need to be considered to set this parameter:

    -   design specifications e.g. max required processing speed
    -   electrical and mechanical properties of the axis (see also
        equation above)
    -   max allowed encoder speed (see encoder data sheet)
    -   cut-off frequency of the encoder input (see drive hardware
        manual)
    -   available DC bus voltage

-   AccelerationMaximum, DecelerationMaximum: This parameters restrict
    the acceleration and deceleration during the move. In most cases the
    same values are used for both parameters. Acceleration and
    deceleration are basically restricted by the max available current
    (see equation above). But also the following factors need to be
    considered:

    -   static load (e.g. vertical axis)
    -   process forces and friction
    -   force restrictions of mechanical elements like spindle drives.

-   DecelerationEmergency: This parameter is relevant if an emergency
    stop is commanded. In normal case the value is set to the same value
    as DecelerationMaximum.

-   JerkMaximum: This parameter defines the maximum slope of the
    acceleration profile. The max possible jerk is basically restricted
    by the available voltage (see equations above). Furthermore the jerk
    limit is also relevant regarding how much the mechanical system is
    excited. A smaller jerk reduces the bandwidth of the excitement and
    will therefore also reduce the position error during the move.
    Typically the vlalue of the jerk limit is set by factor 10 to 100
    bigger than the acceleration maximum.

-   DynamicReductionFactor: The dynamic reduction factor
    **f*<sub>*drf*</sub>* is a value in the range \[0..1\] and can be
    use to reduce the path dynamics. The factor scales the limits
    accordingly the following rules:

|                                                                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                                                                                        
 $${v\_{\text{red}} = v\_{\text{max}}}f\_{\mathit{drf}};\mspace{108mu}{a\_{\text{red}} = a\_{\text{max}}}f\_{\mathit{drf}}^{2};\mspace{108mu}{r\_{\text{red}} = r\_{\text{max}}}f\_{\mathit{drf}}^{3}$$  |

### <span id="anchor-52"></span>Axis\[\].Parameters.PositionController

The position controller node contains registers to configure the
encoder, the position controller and the feed forward. For a normal axis
only Encoder\[0\] and Controller\[0\] need to be configured.
Encoder\[1\] and Controller\[1\] are used if an axis provides a second
encoder, e.g. for dual loop-control.

-   PositionUnit: This parameter is used to define the unit of the
    positions and it ensures that position units in **TAM System
    Explorer** are displayed correctly.  
    With **EtherCAT** this parameter is also used to set the scaling of
    the set-points received from the control system. See
    [\[2\]](#anchor-8) for more information.
-   MasterPositionSource: With this parameters the source for
    Signal.PositionController.MasterPosition can be defined.

The following parameters can be used to configure the feed forward.
Figure shows the diagram of the feed forward block.

-   FeedForwardPosition: This parameter compensates a force which is
    proportional to the position, e.g. a spring. For an initial setup
    this parameter is set to zero in most cases.
-   FeedForwardVelocity: This parameter compensates a viscous friction.
    As the viscous friction is not known in advance, this parameter is
    set to zero for the initial setup.
-   FeedForwardAcceleration: This parameter compensates the inertia of
    the axis. This is an important parameter regarding the dynamic
    performance of the axis. Basically, if the inertia of the axis and
    the torque constant of the motor are known, the parameter could be
    set to:

|                                                                                         |
|-----------------------------------------------------------------------------------------|
|                                                                                         
 $$\mathit{FeedForwardAcceleration} = \frac{\mathit{Inertia}}{\mathit{TorqueConstant}}$$  |

-   But in general it is recommended to set this parameter to zero for
    the initial setup. The parameter can then be set and optimized later
    based on measurements as described in section [5.4.6](#anchor-53).

-   FeedForwardCoulombCurrent: This parameter compensates Coulomb
    friction. Initially this parameter should be set to zero. If
    required, the parameter can then be set later based on measurements.

    <figure>
    <img
    src="gitbook/Pictures/Pictures/10000000000005C4000002F0329128CE38E57942.png"
    style="width:12.285cm;height:5.99cm" alt=" " />
    <figcaption aria-hidden="true"><br />
    </figcaption>
    </figure>

-   FeedForwardCoulombVelocity: With this parameter the transition range
    of the coulomb feed forward can be set. This allows to smooth the
    transition of the current when the direction of the movement is
    changed.

-   FeedForwardFilter: By default the Type of the filter should be set
    to bypassed.

-   OutputLimit: This parameter restricts the output of the position
    controller. Typically this parameter ist about 5-10% below the peak
    current of the motor or the drive, depending on which is smaller.

### Axis\[\].Parameters.PositionController.Encoders

The encoder node contains registers to configure Encoder\[0\] and
Encoder\[1\]. For an axis with only a single encoder only Encoder\[0\]
has to be configured. Encoder\[1\] is used if an axis provides a second
encoder signal, e.g. for dual loop-control.

-   Type: This parameter is set to the encoder type connected to the
    related connector. By default this is connector X20 for Axis\[0\]
    and X21 for Axis\[1\]. Set Type to Analog if the position
    information is provided by a pair of analog sine and cosine signals
    with an amplitude of 1Vpp. See [\[8\]](#anchor-49) for information
    about other supported encoder types. If no encoder is attached to
    the connector, the parameter has to be set to None to avoid an
    EncoderError.

-   InvertDirection: This parameter is used to define the positive
    direction of the position. Set this parameter to True, if the
    positive direction of the encoder position is opposite to the
    positive direction of the physical axis. In case this parameter is
    changed on an already commissioned axis, change the parameter
    Motor.InvertDirection too.

-   Pitch: This parameter defines the scale of the position. If Type is
    Analog or Incremental, the value of Pitch is the distance between
    two encoder lines. Examples:

    -   For a rotational encoder with 2048 lines and with the position
        unit in degree, the Pitch is 360°/2048 = 0.17578125.
    -   <img
        src="gitbook/Pictures/Pictures/10000000000004A0000001FDF536D634983A6962.png"
        title="fig:" style="width:10.68cm;height:5.17cm" alt=" " />For a
        linear encoder the value for Pitch is taken from the data sheet
        of the encoder, e.g. 0.02 for an encoder with a pitch of 20um
        and position units of "mm".If an encoder with digital protocol
        is used refer to [\[8\]](#anchor-49) on how to set the Pitch
        parameter.

-   VelocityFilterT1: With this parameter the bandwidth of
    PositionController.Encoders\[\].Velocity can be defined. The value
    corresponds to the time constant of the filter.

Backlash compensation can be applied if an axis shows a directional
contouring error during slow motion. This can for example be caused by
the backlash of a spindle drive.

<figure>
<img
src="gitbook/Pictures/Pictures/100000000000037C00000121DBB69784797DF42B.png"
style="width:12cm;height:3.87cm"
alt=" Figure 39: Backlash compensation." />
<figcaption aria-hidden="true"><br />
Figure 39: Backlash compensation.</figcaption>
</figure>

-   BacklashDistance: The value of BacklashDistance has to be set equal
    to the value of the contouring error. For dual-loop axes, the
    backlash has to be configured for the encoder of the inner
    controller loop (Encoder\[0\] in most cases). To align the backlash
    compensation with the axis reference, the direction of the reference
    move can be considered for the compensation by setting the sign of
    the parameter:

    -   Use a positive sign if the reference move is done in positive
        direction. In this case the correction is applied when the axis
        is moving in negative direction.
    -   Use a negative sign if the reference move is done in negative
        direction. In this case the correction is applied when the axis
        is moving in positive direction.

-   BacklashDuration: The value of
    Parameters.PositionController.Encoders\[\].BacklashDuration can be
    used to configure the smoothing of the backlash compensation. If
    backlash compensation is applied, a change of direction causes a
    position shift of the actual position. To smoothing this shift, a
    second order low pass filter is applied. The dynamics of this filter
    can be configured with the parameter BacklashDuration. Typical
    values are in range of 0.1 to 0.5s.

    -   A small value causes a fast shift of the position.
    -   A big value causes a slow shift of the position.

****Not****e**** Backlash Compensation is suitable to compensate
contouring errors during slow motion. ****For high dynamic moves the
application of backlash compensation can be counterproductive ****as the
backlash error not only depends on the move direction but also on the
acceleration and deceleration. ****

### Axis\[\].Parameters.PositionController.Controllers

The controller node contains registers to configure Controller\[0\] and
Controller\[1\]. The structure of the controller is described in section
[5.4](#anchor-54). For an axis with a single encoder only
Controller\[0\] has to be configured. Controller\[1\] is only used if an
axis provides a second encoder signal e.g. for dual loop-control.

-   Kp, Ki, Kd, T1: These registers are used to configure the PIDT1
    position controller. For the initial configuration, these values can
    be set to zero. The setup and optimization of the position
    controller is described in section [5.4.3](#anchor-55).
-   PositionErrorLimit: This parameter defines the maximum allowed
    position error. If the position error exceeds this limit, the axis
    is disabled and a PositionErrorLimit error is issued. This is an
    important parameter which helps to protect the machine in case of a
    malfunction. Set this parameter as small as possible without causing
    faulty activation of the error. Typical values are 0.1mm to 0.5 mm
    for linear axes and 0.1 degree to 1.0 degree for rotational axes.
-   IntegratorOutputLimit: This parameter restricts the current of the
    integral term. It is recommended to set this value to about 40% to
    80% of the nominal current.
-   Filters: Filters can be used to optimize the stability of the
    controller loop. See section [5.4.5](#anchor-56) for more
    information. For the initial setup the Type of the filters should be
    set to bypassed.

****Warni****ng**** ****PositionErrorLimit must be configured correctly
before the drive is enabled the first time to protect the axis.

### <span id="anchor-57"></span>Axis\[\].Parameters.Commutation

**Commutation** is the process of applying current to the phases in the
right order to generate motion. For brushed DC-Motors, commutation is
ensured mechanically by contacting the correct winding with the brush.
For synchronous AC motors, commutation has to be performed
electronically, in most cases based on the encoder position.

For electronic commutation it is crucial to initially determine the
orientation between the electrical phases (stator) and the magnetic
poles (rotor). The process to find this orientation is called
**phasing**. With the following parameters, the phasing process can be
configured:

-   PhasingMethod: This parameter selects the phasing method with the
    following choices (see also Figure ):

    -   NoPhasing: This method is used if Axis\[\].Motor.Type = DC or if
        a motor with an absolute encoder is already initialized with the
        correct phasing angle (see section [6.1](#anchor-58)).
    -   RotorAlignment: The rotor is aligned by applying a current to a
        specific phase angle. This causes the rotor to align with the
        magnetic field of the phases. If the rotor is not already
        aligned by chance, this causes a movement of the rotor. This
        method must be used for the initial commissioning of synchronous
        AC-motors as it does not require a tuned position controller.
    -   <img
        src="gitbook/Pictures/Pictures/100000000000056F000001B024678BE526934CDA.png"
        title="fig:" style="width:12.46cm;height:4.623cm" alt=" " />AngleSearch:
        With this method, the electrical direction of the current is
        controlled in such a way, that the motor does not move during
        angle search. This method requires a stable setup of the
        position controller. It is recommended to use this method for
        axes which must not move during phasing and for axes with low
        damping (e.g. for axes with air bearings). As AngleSearch
        requires a tuned position controller it is not suitable for the
        initial setup.

-   EnablingMethod: This parameter specifies if phasing is executed when
    the motor is enabled. In case of an absolute encoder the parameter
    is used to specify the source for the commutation offset. The
    following options can be selected:

    -   ForcePhasing: Phasing is executed at every enabling of the
        motor.
    -   Automatic: Phasing is executed only if
        Axis\[\].Signals.Commutation.State is Invalid. This could for
        example be the case after a power-cycle of the drive. The
        commutation state will change to Valid when phasing is executed
        successfully. This method should not be used before the
        commissioning of the current controller and the position
        controller is successfully done.
    -   NoPhasing: This option is used if Axis\[\].Motor.Type = DC.
    -   AbsoluteEncoder; AbsoluteEncoderOffsetEncoder;
        AbsoluteEncoderOffsetDrive: See section [6.1](#anchor-58) for
        how to setup the commutation based on absolute encoders.

    For an initial setup it is recommended to use ForcePhasing.
    Depending on the application the setting can be changed for example
    to Automatic after the commissioning is successfully done. During
    phasing, a current is applied. The shape of this current can be
    configured with the following parameters (see also Figure ).

-   Angle: This is the electrical angle of the phasing vector used in
    the RotorAlignment method. Default value is zero.

-   StartTime: This parameter delays the start of the phasing. This
    might be useful if a brake with significant delay has to be released
    before the phasing starts. For most applications this parameter is
    set to zero.

-   RampRiseTime: This parameter is used to configure the duration of
    the current ramp. The recommended setting for this parameter depends
    on the PhasingMethod:

    -   RotorAlignment: RampRiseTime typically 1.0-2.0s
    -   AngleSearch: RampRiseTime typically 0.1-0.2s

-   RampConstTime: This parameter should be set to a value which allows
    the axis to reach steady state. Depending on the type of axis this
    is typically 0.5-2.0s. The value has to be increased, if the axis is
    still in motion at the end of the phasing.

-   Current Amplitude: This parameter defines the amplitude of the
    applied current. It is typically set to 50-100% of the nominal
    current.

It is possible that the initial position of the axis is exactly opposite
to the applied current-angle. In this case nearly no torque is applied
to the motor and phasing may fail. To prevent this case, the angle of
the applied current is oscillated three times at the beginning of the
phasing. This should get the axis out of its equilibrium. The following
parameters can be used to configure the oscillation:

-   SineAmplitude: Amplitude of the angular oscillation. Typical values
    are 0.1-0.5rad.
-   <img
    src="gitbook/Pictures/Pictures/1000000000000479000002F6D354A4D6A0B9369A.png"
    title="fig:" style="width:13cm;height:8.691cm"
    alt=" Figure 41: Phasing sequence with Type = RotorAlignment." />SineFrequency:
    Frequency of the angular oscillation. Typical value is 10Hz.

### <span id="anchor-59"></span>Axis\[\].Parameters.CurrentController

This section describes the initial setup of the current controller. The
structure of the controller is described in section [5.4](#anchor-54).

-   PwmFrequency: This parameter is used to define the frequency of the
    pulse width modulation. In most cases this parameter should be set
    to pwm50kHz, as this allows higher drive currents. Only for motors
    with very low impedance (e.g. spindles) pwm100kHz can be considered
    to reduce the heating of the motor.

-   Kr, Tn: These registers are used to configure the PI current
    controller. For initial configuration these values can be set to
    zero. The setup and optimization of the current controller is
    described in section [5.4.1](#anchor-60).

-   IntegratorOutputLimit: This parameter can be used to restrict the
    output of the integral term to avoid a windup behavior of the
    controller. Typically this value is set to 0.5..1.0 of the
    CurrentController.OutputLimit (see below)

-   R, L, Kt: These parameters are the voltage feed forward with R
    representing the phase to phase resistance, L for the phase to phase
    inductance and Kt is the back EMF constant of the motor. In most
    cases it is recommended to set these parameters to zero, as voltage
    feed forward is not required because of the high bandwidth of the
    current controller.

-   FeedForwardLimit: Set this parameter to limit the feed forward
    voltage calculated by the R, L and Kt parameters. If
    FeedForwardLimit is set to zero, the feed forward path is disabled.

-   OutputLimit: This parameter restricts the maximum output voltage
    over one phase. Typically this parameter is set to the maximum
    possible voltage which depends on the available DC-bus voltage and
    the Motor.Type:

    -   SynchronousAC: The maximum setting is 0.577 times the dc-bus
        voltage.
    -   DC: In case of a DC-motor the OutputLimit can be set equal to
        the DC-bus voltage.

### Axis\[\].Parameters.CurrentController.FeedForwardFilter

By default and for a first setup the Type of the filter should be set to
bypassed to deactivate it. Refer to Figure for more information.

### Axis\[\].Parameters.Homing

This node can be used to configure a homing sequence executed by the
drive. More information about how to setup the homing of an axis is
documented in [\[11\]](#anchor-61).

-   Method: For the initial setup of the axis no homing is required and
    the homing method is set to None.

## <span id="anchor-62"></span>Verification of the Encoder

With this test the configured encoder pitch and the encoder direction
are verified. For the test, move the axis by hand for a certain distance
e.g. for one turn and observe the position in the **TAM System
Explorer**. To observe the position the following options are available.

1.  Select the associated axis module in the **Topology Tree** and
    observe the position displayed at the upper right corner of the axis
    module.
2.  Observe the value of the register
    Axes\[\].Signals.PositionController.Encoders\[\].Position in the
    ****Registers**** tab of the tab panel.
3.  Drag the register
    Axes\[\].Signals.PositionController.Encoders\[\].Position into the
    scope area and start the scope.

Check the counting direction and if the relative distance of the
displayed position corresponds to the executed move. If there is a
mismatch, adjust the following parameters and execute the test again.

-   Axes\[\].Parameters.PositionController.Encoders\[\].InvertDirection
-   Axes\[\].Parameters.PositionController.Encoders\[\].Pitch

In case the position signal shows no movement at all, the connection of
the encoder has to be verified. Especially if an option module is used
also check the setting of General.Parameters.EncoderTopology (see
[\[8\]](#anchor-49) for more information).

## <span id="anchor-54"></span>Controller Tuning

After initial configuration of the parameters, the controllers are ready
to be tuned. For the tuning of the controllers the **Bode Tuning
**module provided by **TAM System Explorer** is used (see section
[4.2](#anchor-40)). The following sections show the structure of the
controller and explain how to execute the **Bode Tuning**. For people
with experience in Triamec drive configuration, can lead you through the
tuning procedure.

Figure shows a simplified block-diagram of the implemented controller
structure. The controller structure supports cascaded control with a
**PI** controller for the current and two **PIDT1** controllers for the
position.

<img
src="gitbook/Pictures/Pictures/10000000000004FA000002492F5C4F454D0C5E88.png"
title="fig:" style="width:17.801cm;height:8.174cm"
alt=" Figure 42: Block-diagram of the controller structure with current controller and position controller (simplified)." />For
an axis with one encoder, only Controller\[0\] is used. If a second
encoder is installed, use Controller\[1\] to setup a dual loop
controller. Both, the position controller and the current controller
support feed forward to set the current and the voltage based on the
setpoint trajectory.

### <span id="anchor-60"></span>Current Controller Structure

The controller structure consists of a PI-controller with proportional
gain Kr and integral time constant Tn. Additionally, the integral term
can be restricted to prevent integral wind-up.

<img
src="gitbook/Pictures/Pictures/100000000000053C000000CA06AFBB297225ABD4.png"
title="fig:" style="width:17.801cm;height:2.683cm"
alt=" Figure 43: Block-diagram of the PI current controller (simplified)." /><img
src="gitbook/Pictures/Pictures/10000000000005C6000001EDB6DBF3C92C6A7E30.png"
title="fig:" style="width:11.564cm;height:3.858cm"
alt="Figure 44: Block-diagram of the voltage feed forward." />In some
cases the dynamic of the current loop can be improved by applying
voltage feed forward. Figure shows the block-diagram for voltage feed
forward.

### <span id="anchor-63"></span>Tuning of the Current Controller

This section describes how the proportional gain Kr and the integral
time constant Tn for the current controller can be determined with
**Bode** **Tuning**. See section [5.2](#anchor-43) on how to initially
set up the other parameters in the current controller structure. The
following steps are required to start the tuning:

1.  Make sure, that the controller gain Kr is set to 0 (this step is not
    required if the current controller is already configured with a
    stable setting).
2.  Execute a bode measurement and save the measured data. See section
    [4.3](#anchor-41) on how to do the measurement.
3.  Open the measured data with the **Bode Tuning **application. See
    section [4.4](#anchor-45) on how to open the measurement and how to
    use the application.
4.  To setup the current controller, select the ****Current**** radio
    button in the ****Select Controller**** panel.
5.  Initially, set the controller gain Kr to 1 (if Kr is zero, no
    transfer functions are plotted).

The controller parameters Kr and Tn can now be modified. After each
change of a parameter the **Bode** or **Nyquist** plots are updated. The
**Bode** plot shows the amplitude and the phase of the following complex
transfer functions:

|                                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                                                                                                                        
 $$H\_{r}{{(f)} = \mathit{Kr}}\left( {1 + \frac{1}{s\mathit{Tn}}} \right);\mspace{144mu} H\_{o}{{(f)} = H\_{r}}{(f)}\frac{i}{u}{(f)};\mspace{144mu} H\_{c}{{(f)} = \frac{H\_{o}{(f)}}{{1 + H\_{o}}{(f)}}};\mspace{144mu}{s = j}2\pi f$$  |

with

-   **f**: frequency
-   **H*<sub>*r*</sub>*(f)**: current controller transfer function
-   **H*<sub>*o*</sub>*(f)**: open loop transfer function
-   **H*<sub>*c*</sub>*(f)**: closed loop transfer function
-   **i**/u**(f)**: measured frequency response function between voltage
    and current.

The *Nyquist* plot shows the open loop transfer function
**H*<sub>*o*</sub>*(f)** in the complex area.

The goal for the tuning is to get a stable controller with the following
characteristics (see also Figure and ):

1)  wide bandwidth of **H*<sub>*c*</sub>*(f)**
2)  high amplification in the pass-band of **H*<sub>*o*</sub>*(f)**
3)  sufficient attenuation in the stop-band of **H*<sub>*o*</sub>*(f)**

Therefore, Kr should be increased while Tn is reduced as close to zero
as possible by considering the following criteria. See on how the
parameters influence the curve.

Tuning criteria in **Bode** plot view:

1)  The phase-margin of **H*<sub>*o*</sub>*(f) **should be in range of
    50° to 70°.[^9]
2)  <img
    src="gitbook/Pictures/Pictures/100000000000038D000003A81003D842E8C67C73.png"
    title="fig:" style="width:8.901cm;height:8.35cm"
    alt=" Figure 45: Tuning criteria in Bode view for the current controller." />The
    amplitude of the **H*<sub>*c*</sub>*(f) **should not exceed 1dB
    **over the **w**hole frequency range**.**

Tuning criteria in ****Nyquist**** plot view (Figure ):

1)  **The displayed complex curve of **H*<sub>*o*</sub>*(f) **must be
    outside of the 1.1 circle but as close to it as possible.**
2)  <img
    src="gitbook/Pictures/Pictures/100000000000038B000003A700C65B3A8FCB37C2.png"
    title="fig:" style="width:8.901cm;height:8.34cm"
    alt=" Figure 46: Tuning criteria in Nyquist view for the current controller." />**Following
    the** **complex curve **H*<sub>*o*</sub>*(f) **from low frequency to
    high frequency, the critical point \[-1, 0j\] must be located in the
    region to the left of the curve.

Rule of thumb for an initial setup of the current controller:

1.  Set Kr = 1 and Tn = 0, and activate the ****Bode**** plot view.
2.  With the cross-hair search the frequency *f*<sub>*gc*</sub> where
    **H*<sub>*o*</sub>*(f*<sub>*gc*</sub>*) **has a phase margin of 60°
    (Figure , marker d)).
3.  Read the amplitude *A*<sub>*gc*</sub>* *at frequency*
    f*<sub>*gc*</sub>* *in *dB.*
4.  An initial value for the gain and the time constant can now be
    calculated with the following equations (see also Figure ):

|     |
|-----|
|     |

1.  Use the criteria above to further optimize the current controller.
2.  <img
    src="gitbook/Pictures/Pictures/10000000000004B9000002574503788905B6552D.png"
    title="fig:" style="width:17.801cm;height:8.481cm"
    alt=" Figure 47: Tuning of the current controller. The figure to the left shows the bode plot with Kr = 1 and Tn=0. A phase margin of 60° (angle = -120°) is reached at 2188Hz with a magnitude of -28.6dB. Based on the rule of thumb this would result in Kr = 27 and Tn = 0.0007. The figure to the right shows the further optimized transfer function with Kr=23 and Tn=0.0001." />Press
    the ****C**ommit** button to activate the parameter changes on the
    drive.

### <span id="anchor-55"></span>Position Controller Structure

<img
src="gitbook/Pictures/Pictures/10000000000005380000013DB80EEC5345D9BF6F.png"
title="fig:" style="width:17.801cm;height:4.15cm"
alt=" Figure 48: Block-diagram of the PIDT1 position controller." />Figure
shows the controller structure of the position controller. It consists
of a PIDT1-controller with proportional gain Kp, integral gain Ki and
derivative gain Kd. The bandwidth of the derivative term can be
restricted with the low pass time constant T1. With the
IntegratorOutputLimit wind-up of the integral can be avoided.
Additionally five filters of second order can be configured.

<img
src="gitbook/Pictures/Pictures/100000000000053B000001F618860501C702CF66.png"
title="fig:" style="width:17.801cm;height:6.682cm"
alt=" Figure 49: Block-diagram of the current feed forward." />Figure
shows the block diagram for current feed forward. Beside the feed
forward of position, velocity and acceleration also coulomb friction can
be compensated. The FeedForwardFilter can be used to fine tune the
feed-forward transfer function.

### <span id="anchor-64"></span>Tuning of a Single-Loop Position Controller

****Im****p****ortant**** The current controller (inner loop) has to be
setup before the position controller (outer loop). This is because the
parametrization of the current controller influences the characteristics
of the position controller. The current controller in contrast is
independent of the parametrization of the position controller.

This section describes the tuning of a single loop position
controller[^10]. With single-loop setup, only one position feedback is
used for control.

-   If the loaded **Bode** measurement contains only one encoder signal,
    this signal is automatically used for the tuning. The radio buttons
    ****Position 1 ****/ ****Velocity 1**** are grayed out and
    ****Single Loop**** is set permanently.

-   If the loaded **Bode** measurement contains signals from two
    encoders, ****Single Loop**** is set by default and should only be
    changed for dual-loop control . The signal used for the tuning can
    be selected as follows:

    -   With ****Position 0 ****or ****Velocity 0**** latched, the
        signal from Encoder\[0\] is used.
    -   With ****Position 1 ****or ****Velocity 1**** latched, the
        signal from Encoder\[1\] is used.

This section considers only the first case, as this is the default case
for single-loop position controllers.

****Im****p****ortant**** For synchronous AC motors the measurement of
the transfer function between current and position requires a valid
commutation. In this case the initial (first time) commissioning of the
position controller requires to set  
Parameters.Commutation.PhasingMethod to RotorAlignment and  
Parameters.Commutation.EnablingMethod must **not** be Automatic!  
Additionally the **Bode** measurement has to be executed again after the
first commissioning of the current controller!

To setup the position controller, ****Position 0**** has to be selected
in the ****Select Controller**** panel. The ****Controller Parameter****
panel shows the parameters used to configure the** PIDT1** controller.

Two equivalent controller structures can be selected in the ****Select
Controller Structure**** panel. This selection has no effect on the
behavior of the controller as all structures are internally transformed
to the ****Additive, Gain**** structure, but it allows to select the
structure which is most suitable for the tuning.

-   <img
    src="gitbook/Pictures/Pictures/200000090000217E00001AA108E55C907EB94151.svm"
    title="fig:" style="width:8.271cm;height:6.366cm"
    alt="Figure 50: Controller Parameter with Additive, Gain selected." />****Additive,
    Gain****:  
    Figure shows the parameters used to configure the **PIDT1**
    controller if ****Additive, Gain ****is selected. With this
    structure, the parameters are identical with the controller
    registers in the Topology Tree. The controller output is the sum of
    the integral path weighted with ****Ki****, the proportional path
    weighted with ****Kp****, and differential path weighted with
    ****Kd**** and filtered with a low pass filter with time constant
    ****T1 ****(see also Figure ).

-   <img
    src="gitbook/Pictures/Pictures/200000090000219300001A8CF86CB837EC13D20C.svm"
    title="fig:" style="width:8.359cm;height:6.311cm" />****Additive,
    Time Constant****:  
    Figure shows the parameters used to configure the **PIDT1**
    controller if ****Additive, Time Constant**** ****is selected. In
    this case the integral and derivative terms are weighted by the time
    constants **Tn** and **Tv** and the position error is multiplied by
    **Kr** (see also Figure ).

The following table shows the equation of the two structures and how
****Additive, Time Constant**** is transformed to ****Additive,
Gain****:

|                                                                                                                                                     |                                                                                                                    |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Additive, Gain                                                                                                                                      | Additive, Time Constant                                                                                            |
|                                                                                                                                                     
 $$G\_{r}{{(s)} = \mathit{Kd}}{\frac{s}{\text{T1}{s + 1}} + \mathit{Kp} + \mathit{Ki}}\frac{1}{s}$$                                                   |                                                                                                                    
                                                                                                                                                       $$G\_{r}{{(s)} = \mathit{Kr}}\left( {\frac{\mathit{Tv}s}{\text{T1}{s + 1}} + 1 + \frac{1}{\mathit{Tn}s}} \right)$$  |
|                                                                                                                                                     
 $${\mathit{Kp} = \mathit{Kr}};\mspace{144mu}{\mathit{Ki} = \frac{\mathit{Kr}}{\mathit{Tn}}};\mspace{144mu}{\mathit{Kd} = \mathit{Kr}}\mathit{Tv};$$  |                                                                                                                    |

****Not****e**** In most cases it is recommended and more intuitive to
use ****Additive, Time Constant**** for the tuning of the position
controller.

With the ****Select Filter**** panel up to 5 filters can be configured.
Use the ****Filter Parameter**** panel to set the ****Type****,
frequency ****f\[Hz\]**** and damping ****D\[1\]****. To disable the
filter, the type is set to ****Bypass****. If ****Advanced**** is
checked, the frequency and damping of the numerator and denominator can
be set independent (see also chapter [5.4.5](#anchor-56)).

The **Bode** plots show the following complex transfer functions:

|                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                                                                                
 $$G\_{r}{(f)};\mspace{144mu} G\_{o}{{(f)} = G\_{r}}{(f)}H\_{c}{(f)}\frac{x}{i}{(f)}F\_{0}{(f)}F\_{1}{(f)}...F\_{4}{(f)};\mspace{144mu} G\_{c}{{(f)} = \frac{G\_{o}{(f)}}{{1 + G\_{o}}{(f)}}}$$  |

with

-   **f**: frequency
-   **G*<sub>*r*</sub>*(f)**: position controller transfer function
-   **G*<sub>*o*</sub>*(f)**: open loop transfer function
-   **G*<sub>*c*</sub>*(f)**: closed loop transfer function
-   **H*<sub>*c*</sub>*(f)**: closed loop current controller transfer
    function
-   **x/**i(f)**: measured frequency response current to position
-   **F*<sub>*0*</sub>*(f)F*<sub>*1*</sub>*(f)...F*<sub>*4*</sub>*(f)**:
    filter transfer function

The **Nyquist** plot shows the open loop transfer function
**G*<sub>*o*</sub>*(f)** in the complex area.

The goal for the tuning of the position controller is to get a stable
controller with the following characteristics (Figure and ):

1)  wide bandwidth of **G*<sub>*c*</sub>*(f)**
2)  high amplification in the pass-band of **G*<sub>*o*</sub>*(f) **
3)  sufficient attenuation in the stop-band of **G*<sub>*o*</sub>*(f)
    **(which may require to place some filters)**.**

with the following tuning criteria in ****Bode**** plot view:

1)  The phase-margin of *G*<sub>*o*</sub>*(f)* should be in range of 30°
    to 50°.
2)  <img
    src="gitbook/Pictures/Pictures/100000000000038B0000032992C9389B6D9C47F8.png"
    title="fig:" style="width:8.901cm;height:8.77cm"
    alt=" Figure 54: Tuning criteria in Bode view for the position controller." />The
    amplitude of the **G*<sub>*c*</sub>*(f) **should not exceed
    **2**dB** **(robust)** to 4 **dB **(advanced) **for a **stable**
    controller **behavior **over the **w**hole frequency range**.**

Tuning criteria in ****Nyquist**** plot view:

1)  **The displayed complex curve of **G*<sub>*o*</sub>*(f) **must be
    outside of the 1.**3 **(robust)** to 1.6 **(advanced)** circle but
    as close to it as possible.**
2)  <img
    src="gitbook/Pictures/Pictures/10000000000003330000032A0839AE4E50227A3B.png"
    title="fig:" style="width:8.901cm;height:8.38cm"
    alt="Figure 55: Tuning criteria in Nyquist view for the position controller." />**Following
    the** **complex curve **H*<sub>*o*</sub>*(f) **from low frequency to
    high frequency, the critical point \[-1, 0j\] must be located in the
    region on the left of the curve.

Rule of thumb for an initial setup of the position controller:

1.  Set Kr = 1 and Tn = 0, activate the ****Bode**** plot view and
    ****Additive, Time Constant ****in the **Select Controller
    Structure** panel****.
2.  Choose an initial value for the gain crossover frequency *f*<sub>*gc
    *</sub>[^11]. For a high performance axis with analog encoder,
    *f*<sub>*gc *</sub>is typically in the range of 300Hz to 600Hz. For
    less stiff axes or encoders with low resolution, *f*<sub>*gc*</sub>
    may be reduced to below 100Hz to meet the stability criteria. A good
    starting point is often 200Hz which can be adjusted later
    iteratively.
3.  Based on the selected *f*<sub>*gc*</sub>, initial values for the
    parameters* Tv* and *T1* can be calculated:

|                                                                                                   |
|---------------------------------------------------------------------------------------------------|
|                                                                                                   
 $${\mathit{Tv} = \frac{1}{2f\_{\mathit{gc}}}}\mspace{144mu} T{1 = \frac{1}{20f\_{\mathit{gc}}}}$$  |

1.  The angle plot should now show a sufficient phase margin at
    *f*<sub>*gc* </sub>of more than 30° to 50°. If this is not the case,
    the gain crossover frequency *f*<sub>*gc* </sub>may have to be
    reduced.
2.  Measure the amplitude *A*<sub>*gc*</sub>* *at frequency*
    f<sub>gc</sub> *in *dB *in the bode plot **with the crosshair**. An
    initial value for the gain *Kr* can now be calculated based on the
    measurement:

|                                                      |
|------------------------------------------------------|
|                                                      
 $$\mathit{Kr} = 10^{- \frac{A\_{\mathit{gc}}}{20}}$$  |

1.  The magnitude of *G<sub>o </sub>*should now cross the **0**dB level
    at the frequency *f<sub>gc</sub>*.**
2.  Check the stability of the controller in the Bode and the Nyquist
    plot based on the criteria listed above. If the stability of the
    controller is insufficient reduce *f<sub>gc </sub>*or try to apply
    filters to compensate **unstable resonances.**
3.  **If the stability is sufficient, the **integral** time constant can
    be set **by using the following equation as an initial value.**

|                                                |
|------------------------------------------------|
|                                                
 $$\mathit{Tn} = \frac{1.5}{f\_{\mathit{gc}}}$$  |

1.  Use the criteria above to further optimize the position controller.
    Figure shows a tuned controller and indicates qualitatively the
    effect of the parameter changes on *G<sub>o</sub>(f)* in the
    **Bode** and **Nyquits** plot.
2.  <img
    src="gitbook/Pictures/Pictures/100000000000065D000002D5B63D44A27513D129.png"
    title="fig:" style="width:17.801cm;height:7.451cm"
    alt="Figure 56: Tuned position controller with a gain crossover frequency fgc of 500Hz and a phase margin of 48.2°. The black arrows indicate the effect of parameter changes in Bode and Nyquist plot (qualitatively)." />Press
    the ****C**ommit** button to activate the parameter changes on the
    drive.

### <span id="anchor-56"></span>Filters

Filters can be used to enhance the properties of the controller loop for
example by compensating mechanical resonances. Although filters can
improve the controller loop, filters should be applied cautious for the
following reasons:

-   Controller loops with filters are often more sensitive to changes to
    the axes.
-   Filters increase the complexity of the controller-loop. Therefore a
    robust setting is more difficult to find.
-   Consider that only resonances which violate the stability criterion
    (see section [5.4.4](#anchor-64)) need to be compensated.

The design of a filter should be done with the *Bode* tool based on a
*Bode* measurement. Different filter types can be selected. But in most
cases Notch2 is applied and will be described below.

Only for position measurement with poor resolution (e.g incremental
encoders) Lowpass1 or Lowpass2 are used to smooth the signal. In this
case the frequency **fd** is set 3 to 10 times the bandwidth of the
controller and for Lowpass2 the damping **Dd** is set to 0.7. Consider
that the application of lowpass filters will reduce the phase-margin and
therefore affect the stability of the controller. It is recommended to
verify the stability of the controller with the **Bode** tool after a
filter is modified.

Notch2

The following equation shows the transfer function of the Notch2 filter:

|                                                                                                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                                                                                        
 $$F\_{i}{{(s)} = \frac{\omega\_{d}^{2}}{\omega\_{n}^{2}}}\frac{{s^{2} + 2}D\_{n}\omega\_{n}{s + \omega\_{n}^{2}}}{{s^{2} + 2}D\_{d}\omega\_{d}{s + \omega\_{d}^{2}}}$$  |

with the following relation to the configuration parameters:

|                                                                                    |
|------------------------------------------------------------------------------------|
|                                                                                    
 $$\begin{matrix}                                                                    
 \omega\_{d} & = & {2\pi\text{fd}} & = & {2\pi\text{EdgeFrequencyDenominator}} \\\\  
 D\_{d} & = & \text{Dd} & = & \text{DampingDenominator} \\\\                         
 \omega\_{n} & = & {2\pi\text{fn}} & = & {2\pi\text{EdgeFrequencyNumerator}} \\\\    
 D\_{n} & = & \text{Dn} & = & \text{DampingNumerator} \\\\                           
 \end{matrix}$$                                                                      
 .                                                                                   |

The Notch2 filter can be considered as the product of a *Lowpass2*
defined by *fd* and *Dd* and a *Highpass2* filter defined by fn and *Dn*
(Figure ). The **Highpass2** parameters **fn** and **Dn** define the
location and the sharpness of the notch. The *Lowpass2* is used to
compensate the strong amplification with higher frequencies caused by
the **Highpass2**. As a simple approach, set the parameters as follows:

|                                                         |
|---------------------------------------------------------|
|                                                         
 $$\begin{matrix}                                         
 \text{fn} & = & \text{Frequency\\ to\\ compensate} \\\\  
 \text{Dn} & = & \text{0.01..0.05} \\\\                   
 \text{fd} & = & \text{fn} \\\\                           
 \text{Dd} & = & \text{10\\ Dn} \\\\                      
 \end{matrix}$$                                           
 .                                                        |

<img
src="gitbook/Pictures/Pictures/10000000000001F900000194FD74434CFC8632DF.png"
title="fig:" style="width:12cm;height:9.67cm"
alt=" Figure 57: The Notch2 filter as product of a Highpass2 with fd=1and Dd= 0.2 and a Lowpass2 with fn=1 and Dd=0.01." />When
**Advanced** mode is not checked in the **Filter Parameters** panel,
*fd* and *Dd* are automatically calculated according the equations
above.

Consider the phase drop in the phase plot of Figure below the notch
frequency. This phase drop may reduce the phase margin and could reduce
the stability of the controller. Therefore, the stability of the
controller has to be checked after a filter is added or modified.

<img
src="gitbook/Pictures/Pictures/100000000000036F000001F3A4D8FB6425DE6D27.png"
title="fig:" style="width:17.801cm;height:9.661cm"
alt=" Figure 58: Resonance at 2000Hz which causes an instability of the controller-loop." />Figure
shows a resonance which causes an instability at 2000Hz. In the Nyquist
plot, resonances appear as circles. Figure shows the same transfer
function now with a Notch2 filter applied at 2000Hz. The controller loop
is now stable.

### <span id="anchor-53"></span>Acceleration Feed Forward

A proper setting of the value for FeedForwardAcceleration is very
important to achieve small position errors during high dynamic
movements. The value for FeedForwardAcceleration can also be determined
based on the Bode Measurement:

1.  Open the measured data with the **Bode Tuning **application. See
    section [4.4](#anchor-45) on how to open the measurement and how to
    use the application.
2.  Select **Position 0** in the ****Select Controller**** panel if
    single loop controller is used.
3.  Temporarily set Kr to 1 and all other controller parameters to zero
    within the Bode Tuning application. Also set the filters to
    ****Bypass****. Do not commit these parameters as this setting is
    only used to determine the value for the acceleration feed forward.
4.  At lower frequencies the amplitude in the Bode view of *Gopen*
    should show a linear section with a drop of 40dB per frequency
    decade. Measure the amplitude **A** with the cursor at a frequency
    **f** within the linear section (see also Figure ). The acceleration
    feed forward can be calculated with the following equation.

|                                                                                    |
|------------------------------------------------------------------------------------|
|                                                                                    
 $$\mathit{FeedForwardAcceleration} = \frac{1}{10^{\frac{A}{20}}{({2\pi f})}^{2}}$$  |

1.  Press the Revert button to reset the parameters.
2.  <img
    src="gitbook/Pictures/Pictures/10000000000003FD0000014C6241A249B261BA37.png"
    title="fig:" style="width:17.801cm;height:5.787cm"
    alt=" Figure 60: Calculation of the acceleration feed forward. With a measured amplitude of -65.3dB at 29.8Hz, the acceleration feed forward is set to 0.052." />Set
    and commit the calculated feed forward value in the register
    Axis\[\]/Parameters/PositionController/FeedForwardAcceleration.

## <span id="anchor-67"></span>Verification of the Setup

This section describes how to use the **Axis Module** and the **Scope**
to verify the setup (see also section [3.3](#anchor-22) and
[4.1](#anchor-19)).

### <span id="anchor-44"></span>Motor Direction and Magnetic Pitch

To verify the motor direction and the magnetic pitch, the TestGenerator
is used to apply a rotating current vector, which will move the axis in
positive electrical direction. It is recommended to execute this check
if:

-   The bode measurement shows an unexpected characteristic.
-   The axis goes in an axis error state immediately after the phasing.
-   There is uncertainty if the magnetic pitch is configured correctly.

Preconditions:

-   To rotate a current vector, the current controller needs to be
    configured properly as described in section [5.4.2](#anchor-63).

The following steps are required to run the verification.

-   Prepare the scope by loading the **Scope Configuration** named
    ****Direction Analysis****.

-   Prepare the TestGenerator with the following values.

    -   Frequency: This parameter defines how fast the axis will move
        during the test. For example, if the parameter is set to 0.5Hz,
        it will take 2s to move a distance of one pole pair pitch.
    -   Amplitude: 0
    -   Offset: 50% to 100% of the nominal current
    -   RampTime: 2s
    -   CommutationAngle: 0rad
    -   Temporarily increase
        PositionController.Controllers\[0\].PositionErrorLimit to a
        value bigger than one pole-pair pitch.
    -   Temporarily set the gains Kr, Ki, Kd of the position controller
        to zero to disable the position controller.

-   Enable Axis\[0\], start the scope and set
    Axes\[\].Commands.TestGenerator.Command to
    StartRotatingVectorConstantCurrent and press **Enter**.

****Warni****ng**** ****As soon as StartRotatingVectorConstantCurrent is
committed, the axis will start to move. The value of
TestGenerator.Frequency has to be set slow enough to stop the axis in
time (see next item).

-   If the setup is correct, the axis will now move with the defined
    frequency. To stop the axis, set TestGenerator.Command to Stop and
    press **Enter**. Stop the scope and disable the axis.
-   To verify the motor direction, check if the signals of
    Commutation.Angle and PositionController.Encoders\[0\].Position have
    the same direction (see also ). If the direction is opposite, switch
    the state of the parameter Motor.InvertDirection.
-   To verify the magnetic pitch, check if one electrical turn (2·π) on
    the Commutation.Angle corresponds to the magnetic pitch measured on
    PositionController.Encoders\[0\].Position (see ).
-   Do not forget to reset
    PositionController.Controllers\[0\].PositionErrorLimit and the
    position gains Kr, Ki and Kd.

<figure>
<img
src="gitbook/Pictures/Pictures/10000000000002B20000019ADFB23B259A8F8DCC.png"
style="width:13.471cm;height:7.999cm"
alt="Figure 61: Verification of motor direction and magnetic pitch: The motor direction is correct as the signal of Angle and Position show the same direction. The magnetic pitch is 20 mm according to the measurement." />
<figcaption aria-hidden="true">Figure 61: Verification of motor
direction and magnetic pitch: <em>The m</em>otor direction is correct as
the signal of Angle and Position show the same direction. The magnetic
pitch is 20 mm according to the measurement.</figcaption>
</figure>

### Commutation

To verify the commutation of the axis, the axis should be enabled at
different positions and it should be verified if a move can be executed:

1.  Check if Parameters.Commutation.PhasingMethod is set as desired and
    if Parameters.Commutation.EnablingMethod is **not** set to
    Automatic!
2.  Prepare the scope by loading the **Scope Configuration** named
    ****Phasing Analysis****.
3.  Start the scope and enable the axis.
4.  Check the scope if the characteristic of the signals is as expected.

-   -   If Commutation.Commutation.PhasingMethod is RotorAlignment:

        -   Check if the current ramp of ActualCurrentD is applied as
            expected.
        -   Check if the position signal shows an alignment move.
        -   Axes with low friction (e.g. with air-bearings) could show a
            slow oscillation during the phasing which could lead to an
            invalid commutation. In this case the PhasingMethod should
            be changed to AngleSearch and the commutation parameters
            should be adjusted accordingly (see section
            [5.2.7](#anchor-57)).

    -   If Commutation.PhasingMethod is AngleSearch:

        -   Check if the current ramp of ActualCurrentQ and
            ActualCurrentD is applied as expected.
        -   Check if the position signal shows only a minor motion.
        -   Check if the position shows no instability and the position
            error is zero at the end of the phasing. If the error is not
            zero, try to reduce Parameters.Commutation.RampRiseTime and
            verify the stability of the position controller. Consider
            switching the PhasingMethod back to RotorAlignment to verify
            the position controller with a new **Bode** measurement.

    -   No loud noises should be heard during phasing.

1.  Check if the axis is stable by manually applying torque to the axis
    if possible.
2.  Reduce the ****Acc.**** and ****Vel.**** values in the ****Axis
    Module****, start the scope and execute a move of at least one
    electrical turn.
3.  Repeat this sequence at different positions.
4.  If the phasing works as expected,
    Parameters.Commutation.EnablingMethod can be set to Automatic.

****Not****e**** ****If the axis goes into error state immediately after
the phasing sequence or ****at the start of a ****move, the
****parameter ****MotorInvertDirection ****might be****
****incorrect****. ****Also verify ****Parameters.Motor.PolePairs****
and ****Parameters.Motor.EncoderCountsPerMotorRevolution (see also
section [5.5.1](#anchor-44))****.****

### Position Controller

If the commutation works as expected, the controller setup can be
verified in time domain. In the following, two different approaches are
described with which a setpoint can be generated:

Test Generator

If registers in node Commands.TestGenerator are configured accordingly,
a square wave can be added to the position setpoint. By measuring the
position or the position-error the step answer can be analyzed. The step
size (amplitude) of the test signal has to be small enough, to not
exceed the output limits of current and voltage. Therefore step answer
is especially useful to analyze the small signal behavior and the
stability of the controller.

1.  Prepare the scope by loading the **Scope Configuration** named
    ****Position Controller Disturbance Tuning****.
2.  Increase the value of
    Parameters.PositionController.Controllers\[\].PositionErrorLimit
    temporarily to not cause an error during the test.
3.  Start the scope.
4.  Enable the axis for example by using the ****Axis Module****.
5.  Prepare the test generator: Frequency: 5Hz, Offset: 0, RampTime: 0.
    Amplitude: The amplitude should be set to a small value to not
    exceed the limits of current or voltage.
6.  Start the test signal by setting Commands.TestGenerator to
    StartPositionSquare.

Axis Module

With the axis module, a move can be executed which is generated by the
internal path planner with restriction of velocity, acceleration and
jerk. Therefore this test is useful to analyze the process related
stability and behavior of the axis and the settings of the feed forward.

1.  Prepare the scope by loading the **Scope Configuration** named
    ****Position Controller Follower Tuning****.
2.  Prepare the ****Axis Module****: Setup a reasonable move between A
    and B. Activate the ****Loop After**** check-box and set a wait time
    of about 500ms. Reduce the dynamic by adjusting the ****Acc.**** and
    ****Vel.**** values in the ****Axis Module.****
3.  <img
    src="gitbook/Pictures/Pictures/1000000100000418000001DDDA0B0179C51C310B.png"
    title="fig:" style="width:17.801cm;height:8.079cm"
    alt=" Figure 62: The Bode plot shows an insufficient phase margin at about 200Hz which is caused by a too aggressive setup of the integral. In time domain this causes oscillations of the position at 200Hz." />Start
    the scope and execute moves by pressing ****Move AB****. Check the
    transient response of the signals. Slowly increase the dynamic
    settings.

If the position error shows oscillations of a certain frequency, check
the Bode plot for a reason of the oscillation (see also Figure and ).
Try to adjust the parameters to increase the damping (increase phase
margin) or reduce the amplitude. Consider applying filters to damp the
oscillation.

If the position error increases when a certain velocity is reached, the
limit for the voltage output might have been reached (see also
OutputLimit of the current controller in [5.2.8](#anchor-59)).

If the position error increases when a certain acceleration is reached,
the limit for the current output might have been reached (see also
OutputLimit of the position controller in [5.2.4](#anchor-52) ).

### Acceleration and Velocity Feed forward.

The following setup is used to verify the acceleration feed forward (see
also [5.4.6](#anchor-53)):

1.  Prepare the scope by loading the **Scope Configuration** named
    ****Feed Forward Analysis****.
2.  Prepare the ****Axis Module****: Setup a reasonable move between A
    and B. Activate the ****Loop After**** check-box and set a wait time
    of about 500ms.
3.  Start the scope and execute moves by pressing ****Move AB****.

<img
src="gitbook/Pictures/Pictures/10000000000004DC000001BC59D6B10B37CA5DC9.png"
title="fig:" style="width:17.801cm;height:6.354cm"
alt=" Figure 64: Feed forward signal with only acceleration feed forward (left) and with additional velocity feed forward (right)." />If
the acceleration feed forward is correctly configured, the
FeedForwardCurrent should match the acceleration related part of
ActualCurrentQ and the position error becomes much smaller compared to
without acceleration feed forward. In some cases also velocity feed
forward has to be added to get a good match.

# <span id="anchor-6"></span>Advanced Topics

This chapter handles topics which are not part of the basic setup of an
axis described in chapter [5](#anchor-5).

## <span id="anchor-58"></span>Commutation with Absolute Encoders

For the commutation of a synchronous AC motor the angle between the
magnetic field of the rotor and the stator windings needs to be known.
With relative encoders, this angle has to be determined at least after
each restart of the drive which is called *Phasing *(see also section
[5.2.7](#anchor-57)). With absolute encoders, the commutation angle does
not change relative to the encoder position and therefore the phasing
has to be executed only once. The resulting commutation angle can then
be stored and reused after each restart. The following absolute encoder
protocols are supported:

-   Endat
-   BissB
-   Tamagawa
-   Nikon

This section describes how to setup the commutation with absolute
encoders and how the commutation angle can be saved to the drive or to
the encoder.

****Not****e**** ****Consider that mechanical adjustments of the encoder
or the motor or replacement of the encoder, motor or the drive affect
the commutation angle and may require ****an**** execution of a
phasing-sequence ****to**** ****re****sto****re**** the commutation
angle. ****

### EnablingMethod

The parameter Commutation.EnablingMethod allows to define how the
commutation angle is derived from the absolute encoder. The following
options are available:

-   -   AbsoluteEncoder: In this case the commutation angle is directly
        derived from the absolute position of the encoder. This case
        requires a preset of the encoder by the manufacturer of the
        motor or by the user (see section [6.1.2](#anchor-68)).
    -   AbsoluteEncoderOffsetEncoder: In this case the commutation
        offset is loaded from the encoder memory. This requires a
        successful initial phasing of the axis followed by storing the
        offset to the encoder (see section [6.1.3](#anchor-69)).
    -   AbsoluteEncoderOffsetDrive: In this case the commutation offset
        is loaded from the drive memory. This requires a successful
        initial phasing of the axis followed by storing the
        configuration persistent on the drive (see section
        [6.1.4](#anchor-70)).

### <span id="anchor-68"></span>Set Absolute Encoder Zero equal to Commutation Zero

The following steps are required to set the encoder zero equal to the
commutation zero:

1.  The commutation sequence has to be set to RotorAlignment in
    Axes\[\].Parameters.Commutation (see also section
    [5.2.7](#anchor-57)).
2.  Execute the phasing-sequence by executing the command
    Axes\[\].Commands.Commutation.Command = StartPhasingAndZeroEncoder.
3.  Check if Axes\[\].Signals.Commutation.State is Valid. If State is
    **not** Valid, check the configuration, especially the commutation
    settings, and restart the phasing-sequence.
4.  To activate commutation based on the absolute encoder set
    Axes\[\].Parameters.Commutation.EnablingMethod to AbsoluteEncoder.

### <span id="anchor-69"></span>Save Commutation Offset to the Encoder

The following steps are required to save the commutation offset to the
encoder:

1.  The commutation sequence has to be configured correctly in
    Axes\[\].Parameters.Commutation (see also section
    [5.2.7](#anchor-57)).
2.  Execute the phasing-sequence by executing the command
    Axes\[\].Commands.Commutation.Command = StartPhasingAndSaveEncoder.
3.  Check if Axes\[\].Signals.Commutation.State is Valid. If State is
    **not** Valid, check the configuration, especially the commutation
    settings, and restart the phasing-sequence.
4.  To use the commutation offset from the encoder set
    Axes\[\].Parameters.Commutation.EnablingMethod to
    AbsoluteEncoderOffsetEncoder.

### <span id="anchor-70"></span>Save Commutation Offset to the Drive

The following steps are required to save the commutation offset to the
drive:

1.  The commutation sequence has to be configured correctly in
    Axes\[\].Parameters.Commutation (see also section
    [5.2.7](#anchor-57)).
2.  Execute the phasing-sequence either

-   -   by enabling the axis with the axis module (see
        [4.1](#anchor-19)) or
    -   by executing the command Axes\[\].Commands.Commutation.Command =
        StartPhasing.

1.  Check if Axes\[\].Signals.Commutation.State is Valid. If **not**
    Valid, check the commutation settings and restart the
    phasing-sequence.
2.  To use the commutation offset from the drive set register
    Axes\[\].Parameters.Commutation.EnablingMethod to
    AbsoluteEncoderOffsetDrive.
3.  If Axes\[\].Signals.Commutation.State is Valid save the
    configuration persistent on the drive (see section
    [3.5.1](#anchor-30)) to store the commutation offset.

### How the Commutation Offset is Derived

During startup of an encoder, the axis checks if the parameter
axes\[\].Parameters.Commutation.EnablingMethod requires taking the
commutation offset from any absolute encoder:

-   AbsoluteEncoderOffsetDrive: try getting the offset from the
    persisted drive data.
-   AbsoluteEncoderOffsetEncoder: try getting the offset from the
    encoder name plate.

If this is successful, the commutation state will be Valid and enabling
will be performed without phasing.

If this fails, the axis will issue the error
NoDigitalEncoderPersistency, which can be acknowledged. The next
enabling will then depend on the parameter
axes\[\].Parameters.Commutation.PhasingMethod. If this is NoPhasing,
enabling will throw an error. Otherwise, the specified phasing method is
executed and enabling is possible.

With this concept, the user can specify, how the drive should behave in
case of a missing absolute commutation information.

### Signals and States

Beside the parameters used to configure phasing different commands and
signals are provided to analyze and debug the phasing sequence.

Axes\[\].Commands.Commutation.Command: This register can be used to
control the phasing state and to save the commutation angle to the
encoder (if supported by the encoder[^12]).

-   Invalidate: Sets the commutation state to Invalid which forces a
    phasing sequence (if specified) when the axis is enabled next time.
-   StartPhasing: Starts a phasing sequence as specified by the
    commutation parameters. StartPhasing can be executed whether the
    axis is enabled or disabled. After a successful phasing, the
    commutation offset is written to the register
    Axes\[\].Signals.Commutation.OffsetAngle, the commutation state is
    set Valid and the axis state will return to the state before the
    phasing.
-   StartPhasingAndSaveEncoder: Same as StartPhasing but additionally
    the commutation offset is saved persistent to the encoder. If
    EnablingMethod is set to AbsoluteEncoderOffsetEncoder this offset
    will be used for the commutation after a power cycle of the drive.
-   StartPhasingAndZeroEncoder: Same as StartPhasing but additionally
    the zero of the absolute encoder is set equal to the zero of the
    commutation angle. This will cause a shift of the position. In case
    the zero of the encoder is equal to the zero of the commutation
    angle it is possible to set the parameter Commutation.EnablingMethod
    to AbsolutEncoder.
-   InvalidateEncoder: This command marks the commutation offset saved
    on the encoder as invalid. After a power cycle of the drive, the
    commutation state will be Invalid.

Axes\[\].Signals.Commutation.State: This register displays the current
phasing state.

-   Disabled: The motor type and angle search method chosen do not
    require angle search (e.g. DC-motor).
-   Invalid: A valid commutation angle is not yet set. This will force a
    phasing when the axis is enabled next time.
-   Phasing: The phasing sequence is ongoing.
-   Hold: The phasing is frozen to allow saving of the commutation
    offset to the encoder.
-   Valid: Any phasing was successful or the commutation offset was
    successfully derived from an absolute encoder depending on the
    EnablingMethod parameter. In both cases the commutation offset is
    written to the register Axes\[\].Signals.Commutation.OffsetAngle.

Axes\[\].Signals.Commutation.Angle: The commutation angle describes the
magnetic field of the rotor relative to the stator-coils (Figure ). The
commutation angle runs from -pπ to pπ, where p is the number of pole
pairs.

<figure>
<img
src="gitbook/Pictures/Pictures/10000000000001FD000001AD7902E719A6321FB5.png"
style="width:6.001cm;height:5.061cm"
alt=" Figure 65: Commutation angle for a rotor with one pole pair." />
<figcaption aria-hidden="true"><br />
Figure 65: Commutation angle for a rotor with one pole
pair.</figcaption>
</figure>

Axes\[\].Signals.Commutation.OffsetAngle: The commutation offset is the
angle between the encoder position and the zero of the commutation
angle. This is the value evaluated during the phasing sequence.

Axes\[\].Signals.PositionController.Encoders\[\].DigitalEncoder.PersistencyCommutationOffset:
This register displays the commutation offset stored on the encoder.

Axes\[\].Signals.PositionController.Encoders\[\].DigitalEncoder.DebugInfo:
Commutation offset is valid if bit 2 of this register is set.

# <span id="anchor-7"></span>Tria-Link Observer

This section describes how the **Tria-**L**ink** can be accessed with
the **TAM System Explorer** while other applications like **TwinCAT**
use the **Tria-**L**ink** adapter.

There are three options to access the **Tria-**L**ink**:

-   use a **Tria-Link **observer card
-   use an *USB *O*bserver*
-   access a **Tria-Link **device with Ethernet and use the device as a
    bridge between **Ethernet** and **Tria-Link **(see
    [\[4\]](#anchor-12)).

The following section describes the first two methods in detail.

<figure>
<img
src="gitbook/Pictures/Pictures/1000000100000B8900000711294234FFAF3DE19B.png"
style="width:9.999cm;height:6.121cm"
alt=" Figure 66: System with observer and USB observer" />
<figcaption aria-hidden="true"><br />
Figure 66: System with observer and USB observer</figcaption>
</figure>

## <span id="anchor-71"></span>USB Observer

The USB observer consists of a *TL* or *TL-DMA* adapter card connected
with an USB cable to a second PC or to the master PC. The USB cable can
be attached to the adapter card without interrupting the system.

With the **TAM System Explorer** running on the PC connected with the
USB cable, the user can perform all setup and analysis operations
described in the former chapters in the same way as they can do with the
Master communication board. They can also observe any drive signals
online, even while the Master Application is running.

If the USB cable is connected to a second PC no extra configuration is
needed when operating **TAM System Explorer** with an **USB Observer**.
If the USB cable is connected to the master PC, ****File \> Prefereces
\> Startup \> Acquired adapters**** should be set to ****Triamec Devices
over USB****. This prevents the TAM System Explorer from accessing the
PCI board that is already occupied by the control system.

## <span id="anchor-72"></span>Observer Card

To observe the **Tria-Link** it is possible to install an additional PCI
based *Tria-Link* adapter card (typically into a 2<sup>nd</sup> PC) and
integrate the adapter card into the *Tria-Link* ring. Any type of
*Tria-Link* adapter card can be used in this case.

<img
src="gitbook/Pictures/Pictures/20000007000023A900001C1E6AD8193481255539.svm"
title="fig:" style="width:7.059cm;height:5.784cm"
alt="Figure 67: Adapter configuration" />As there is no dedicated
observer adapter card, the adapter card has to be configured as observer
card. In order to set up the system in observer mode the following steps
have to be executed:

1.  Add the PC with the **Tria-Link** adapter card to the **Tria-Link
    **ring.
2.  Start **TAM System Explorer** on the observer PC.
3.  Set the **Adapter** to ****Observer ****(Figure ). This setting is
    lost after a restart of the PC.
4.  Press OK in the following two “Tria-Link Adapter Reset
    Configuration” and “Tria-Link Adapter Reset Warning” dialogs.
5.  Perform ****File \> ****Identify**** on the Observer PC.

# <span id="anchor-46"></span>Flow Charts

<figure>
<img
src="gitbook/Pictures/Pictures/10000001000006EC00000C98F7005558292A8B45.png"
style="width:10.273cm;height:18.692cm"
alt="Figure 68: Initial Setup Guide Workflow" />
<figcaption aria-hidden="true">Figure 68: Initial Setup Guide
Workflow</figcaption>
</figure>

<figure>
<img
src="gitbook/Pictures/Pictures/10000001000006A80000087847A6413CD622A034.png"
style="width:17.801cm;height:22.648cm"
alt="Figure 69: Position Controller Tuning Workflow" />
<figcaption aria-hidden="true">Figure 69: Position Controller Tuning
Workflow</figcaption>
</figure>

# <span id="anchor-73"></span>References

1.  <span id="anchor-24"></span>“Data Export and Import in
    TAM System Explorer Application Note”,  
    AN132_TamSystemExplorerDataExchange_EP006.pdf, Triamec Motion AG,
    2022
2.  <span id="anchor-8"></span>"Triamec TwinCat Quick Startup Guide”,
    SWTC_TwinCAT-UserGuide_EP024.pdf, Triamec Motion AG, 2016
3.  <span id="anchor-9"></span>“Triamec TwinCat Ethercat Quick Startup
    Guide”, SWTC_TwinCAT-UserGuideEcat_EP005.pdf, Triamec Motion AG,
    2019
4.  <span id="anchor-12"></span>“Ethernet Interface”,
    AN123_Ethernet_EP004.pdf, Triaemc Motion AG, 2022
5.  <span id="anchor-35"></span>“TAM API Developer Manual”,
    SWNET_TamApiDeveloperManual_EP033.pdf, Triamec Motion AG, 2019
6.  <span id="anchor-36"></span>“Tama Compiler User Guide”,
    SWTAMA_CompilerUserGuide_EP026.pdf, Triamec Motion AG, 2019
7.  <span id="anchor-39"></span>“Axis Coupling in TAM System Explorer
    Application Note”,  
    AN131_TamSystemExplorerAxisCoupling_EP002.pdf, Triamec Motion AG,
    2022
8.  <span id="anchor-49"></span>“Encoder configuration for the TSD drive
    series”, AN107_Encoder_EP017.pdf,  
    Triamec Motion AG, 2022
9.  <span id="anchor-74"></span>“Sensorless Motor Commissioning User
    Guide”,  
    AN133_SensorlessCommissioning\_­UserGuide_EP005.pdf, Triamec Motion
    AG, 2022
10. <span id="anchor-65"></span>"Dual-Loop Controller with Screw Drive",
    AN138_DualLoopControllerWithScrewDriveAxis_EP006.pdf, Triamec Motion
    AG, 2022
11. <span id="anchor-61"></span>“Homing Procedures and Setup”,
    AN141_HomingProceduresAndSetup_EP002.pdf, Triamec Motion AG, 2022
12. <span id="anchor-66"></span>“MIMO Gantry Commissioning”,
    AN139_MIMOGantryCommissioning_UserGuide_EP004.pdf, Triamec Motion
    AG, 2022

# <span id="anchor-75"></span>Revision History

<table>
<tbody>
<tr class="odd">
<td>004</td>
<td>2020-03-02</td>
<td>dg</td>
<td>Section <a href="#anchor-51">5.2.3</a> modulo settings fixed.</td>
</tr>
<tr class="even">
<td>005</td>
<td>2020-04-20</td>
<td>dg</td>
<td>Description for brake release added in section <a
href="#anchor-50">5.2.2</a>.</td>
</tr>
<tr class="odd">
<td>006</td>
<td>2020-09-09</td>
<td>dg, chm</td>
<td>Description of CurrentController.OutputLimit and
CurrentController.IntegratorOutputLimit corrected. GUI changes
adapted.</td>
</tr>
<tr class="even">
<td>007</td>
<td>2021-02-05</td>
<td>bl</td>
<td>New File Name and Product Nomenclature, various edits</td>
</tr>
<tr class="odd">
<td>008</td>
<td>2021-03-25</td>
<td>dg</td>
<td>Save Tama to configuration modified; parameters VelocityFilterT1 and
MasterPositionSource added.</td>
</tr>
<tr class="even">
<td>009</td>
<td><p>2021-04-01</p>
<p>2021-04-14</p></td>
<td><p>chm</p>
<p>chm</p></td>
<td><p>Subscription registers moved into internal signals. Revise
section <a href="#anchor-32">3.7</a>.</p>
<p>GUI changes adapted.</p></td>
</tr>
<tr class="odd">
<td>010</td>
<td>2021-08-09</td>
<td>bl</td>
<td>Section <a href="#anchor-42">4.3.1</a> Added
Axes[i]/Parameters/PositionController/OutputLimit to required
configuration</td>
</tr>
<tr class="even">
<td>011</td>
<td>2021-08-16</td>
<td>dg</td>
<td>Rule of thumb adjusted in section <a href="#anchor-60">5.4.1</a> and
<a href="#anchor-64">5.4.4</a>.</td>
</tr>
<tr class="odd">
<td>012</td>
<td>2021-08-31</td>
<td>chm</td>
<td>Root topology no longer shown in view</td>
</tr>
<tr class="even">
<td>013</td>
<td>2021-11-22</td>
<td>sm</td>
<td>Document review, updates and corrections</td>
</tr>
<tr class="odd">
<td>014</td>
<td>2022-01-14</td>
<td>chm</td>
<td>TAM System Explorer now has PCI access excluded in the default
configuration</td>
</tr>
<tr class="even">
<td>015</td>
<td>2022-04-04</td>
<td>sm</td>
<td>Update references, insert Flow Charts, minor fixes.</td>
</tr>
<tr class="odd">
<td>016</td>
<td>2022-05-13</td>
<td>sm</td>
<td>Insert the usage of scope templates, describe soft limit registers,
minor updates</td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

[^1]: Communication is suspended after a soft reboot of a drive with
    persistent link address observed via Tria-Link, or after an
    initialize of the Tria-Link executed by another control system.

[^2]: *OverrideControlSystem* needs only to be set with certain link
    protocols e.g. *EtherCAT*.

[^3]: If the plots are empty, the controller gain may be zero. Set the
    gain to a value \>0 in this case.

[^4]: Important: Consider if the current is given as peak value or as
    root mean square value (RMS). Contact the manufacturer of the motor
    if this is not declared in the data sheet.

[^5]: Similar symptoms are caused by incorrect configuration of
    InvertDirection, EncoderCountsPerMotorRevolution and PolePairs (see
    also section [5.5.1](#anchor-44)).

[^6]: IncrementalRS422; IncrementalTTL; Analog; AnalogEndat;AnalogBissB:

[^7]: DigitalEndat; DigitalBissB; DigitalTamagawa; DigitalNikon

[^8]: The DirectCoupledMotion state expects valid triplets of
    Position-Velocity-Acceleration data. In the illegal case where
    triplets contain velocity=0, the software limit feature will not
    work properly.

[^9]: The phase-margin is the difference between the phase-angle of a
    transfer function *G*<sub>*o*</sub>*(f*<sub>*gc*</sub>*)* at the
    frequency *f*<sub>*gc*</sub> where the amplitude of
    *H*<sub>*o*</sub>*(f*<sub>*gc*</sub>*)* crosses 0dB and -180°. See
    d) in Figure .

[^10]:  For other typologies see application note [\[10\]](#anchor-65)
    for dual loop axes and [\[12\]](#anchor-66) for gantry axes.

[^11]: The gain crossover frequency *f*<sub>*gc*</sub> is the frequency
    at which the gain of the tuned controller crosses 0dB.

[^12]: Endat; BissB; Tamagawa; Nikon
