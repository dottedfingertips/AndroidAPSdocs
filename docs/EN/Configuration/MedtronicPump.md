# Medtronic Pumps

***

The Medtronic pump driver only works with older pump models.  The driver does not work with newer models such as the 640G, 670G or 780G.

The following model and firmware combinations are compatible:

    - 512/712 (any firmware version)
    - 515/715 (any firmware version)
    - 522/722 (any firmware version)
    - 523/723 (firmware 2.4A or lower)
    - 554/754 EU release (firmware 2.6A or lower)
    - 554/754 Canada release (firmware 2.7A or lower)

You can find out how to check the firmware on the pumps at [OpenAPS docs](https://openaps.readthedocs.io/en/latest/docs/Gear%20Up/pump.html#how-to-check-pump-firmware-check-for-absence-of-pc-connect) or [LoopDocs](https://loopkit.github.io/loopdocs/build/step3/#medtronic-pump-firmware).

***
QUESTION - IS THIS STILL NEEDED?
If you started using Medtronic driver please add yourself to this [list](https://docs.google.com/spreadsheets/d/16XIjviXe8b-12PrB6brGubNFuAEsFZr10pjLt_SpSFQ/edit#gid=0). This is just so that we can see which Phones are good and which are not so good (or bad) for this driver. There is one column called "BT restart". This is to check if yourPhone supports BT enable/disable, which can be used when pump is no longer able to connect, that happens from time to time. If you notice any other problem, please write that in Comments column.

***

## Hardware and software requirements
- **Phone:** The Medtronic driver should work with any android phone that supports Bluetooth connections. **IMPORTANT: Phone manufacturers Bluetooth implementations can vary so how each phone model behaves can vary.  For example, some phones will handle enabling/disabling Bluetooth differently.  This can impact the user experience when AAPS needs to reconnect to your Rileylink type device.**
- **RileyLink Compatible Device:** Android phones cannot communicate to Medtronic pumps without a seperate device to handle communications. This device will link with your phone via Bluetooth and with your pump via a compatible radio connection.  The first such devlice was called a Rileylink but a number of other options are now available which can offer additional functionality.

    - Rileylink available at [getrileylink.org](https://getrileylink.org/product/rileylink916)
    - Orangelink available at [getrileylink.org](https://getrileylink.org/product/orangelink)
    - Emalink (multiple model options) available at [github.com](https://github.com/sks01/EmaLink)

A comparision chart for the various Rileylink compatible devices can be found at [getrileylink.org](https://getrileylink.org/rileylink-compatible-hardware-comparison-chart?fbclid=IwAR2vHbOzla-zmM-cSp4NkOB_23k3spgnaYvCIGRcACcIQ25FJAU_7HRkH2A)

QUESTION - KEEP GNARL?

## Configuration of the pump
The following settings should be configured on the pump in order for AAPS to remotely send commands.  The steps necessary to make each change on a Medtronic 715 are shown in brackets for each setting.  The exact steps may vary based on pump type and/or firmware version.

- **Enable remote mode on Pump** (On the pump press Act and go to Utilities -> Remote Options, Select On, and on next screen do Add ID and add any random id such as  111111). At least one ID must be on the Remote ID list in order for the pump to expect remote communication.
- **Set Max Basal** (On the pump press Act and got to Basal and then select Max Basal Rate) As an example setting this value to four times your maximum standard basal rate would allow a 400% Temporary Basal Rate. The maximum value permitted by the pump is 34.9 units per hour.
- **Set Max Bolus** (On the pump press Act and to to Bolus and then select Max Bolus) This is the largest bolus that the pump will accept.  The maximum value permitted by the pump is 25.
- **Set profile to Standard**. (On the pump press Act and go to Basal and then Select Patterns) The pump will only need one profile as AAPS will manage different profiles on your phone.  No other patterns are required.
- **Set Temporary Basal Rate type** (On the pump press Act and go to Basal and then Temp Basal Type).  Select Absolute (not Percent).
 

## Medtronic Configuration of Phone/AndroidAPS
- **Do not pair RileyLink compatible device with the Bluetooth menu on your phone.** Pairing via the Bluetooth menu on your phone will stop AndroidAPS from seeing your Rileylink Compatible device when you follow the instructions below. 
- Disable automatic screen rotation on your phone.  On certain devices automatic screen rotation causes Bluetooth sessions to restart which would cause issues for your Medtronic pump. 
- There are two ways to configure your Medtronic pump in AndroidAPS: 
1. Using the setup wizard as part of a fresh install
2. By selecting the cog icon beside the Medtronic selection in the pump selection option in Config Builder

When configuring your Medtronic pump with the setup wizard it is possible that you will be prevented from completing setup because of Bluetooth issues (e.g. you cannot succesfully connect to the pump).  Should this happen you should select the virtual pump option in order to complete the configuration and allow for further troubleshooting by using option 2.  

![Medtronic Settings](../images/Medtronic01a.png)

While setting up AndroidAPS to work with your medtronic pump you need to set following items: (see picture above)
- **Pump Serial Number**: Displayed on the back of your pump and starts with SN. You should only enter the 6 numbers shown without any alpabetic characters (e.g. 123456).
- **Pump Type**: The model pump you are using (e.g. 522). 
- **Pump Frequency**: There are two options based on where your pump was originally distributed.  Please check the FAQ if you are unsure which option to select  [FAQ](../Configuration/MedtronicPump#faq)):
    - for US & Canada, frequency used is 916 Mhz
    - for Worldwide, frequency used is 868 Mhz
- **Max Basal on Pump (U/h)**: This needs to match the setting set on your pump (see Configuration of the pump above).  Again this setting must be carefully selected as it will determine how much AndroidAPS can deliver via your basal rate.  This will effectively set the maximum temporary basal rate.  As an example setting this value to four times your maximum standard basal rate would allow a 400% Temporary Basal Rate. The maximum value permitted by the pump is 34.9 units per hour.
- **Max Bolus on Pump (U)** (in an hour): This needs to match the setting set on your pump (see Configuration of the pump above).  This setting should be carefully considered as it determines how large a bolus AndroidAPS can ever set.
- **Delay before Bolus is started (s)**: The number of seconds after a bolus is issued before the command is actually sent to the pump.  This period of time allows the user to cancel the bolus in the event a bolus command is sent in error.  It is not possible to cancel a bolus that has started via AndroidAPS.  The only way to cancel a bolus that has already started is to suspend the pump manually followed by resuming it.
- **Medtronic Encoding**: Determines if the medtronic encoding is carried out.  Selecting Hardware encoding (i.e. carried out by the Rileylink compatible device) is preferred as this results in less data being sent.  Selecting Software encoding (i.e. carried out by AndroidAPS) can help in the event frequent disconnects are seen. This setting will be ignored if you have firmware version 0.x on Rileylink devices.
- **Battery Type (Power View)**: In order to correctly determine the remaining battery power level you should select the type of AAA battery in use. When a value other than simple view is selected AndroidAPS will display the remaining calculated battery percentage level and volts. The following options are available:

    - Not selected (Simple view)
    - Alkaline (Extended view)
    - Lithium (Extended view)
    - NiZn (Extended view)
    - NiMH (Extended view)

- **Bolus/Treatments Debugging**:  Select On or Off depending on requirements.
- **RileyLink Configuration**: This option allows you to find and pair your Rileylink compatible device.  Selecting this will show any nearby Rileylink compatible devices and the signal strength.
- **Use Scanning** Activates Bluetooth scanning before connecting with your Rileylink Compatible devices.  This should improve the reliability of your connection to the device.
- **Show battery level reported by OrangeLink/EmaLink/DiaLink** This feature is only supported on newer link devices such as the EmaLink or OrangeLink. Values will be shown in the Medtronic tab in AnroidAPS. 
- **Set neutral temp basals** By default Medtronic pumps beep on the hour when a temporary basal rate is active.  Enabling this option can help reduce the number of beeps heard by interupting a temporary basal at the hour change in order to supress the beep.

## MEDTRONIC (MDT) Tab
![MDT Tab](../images/Medtronic02.png)
When AndroidAPS is configured to use a Medtronic pump a MDT tab will be shown in the list of tabs at the top of the screen.  This tab displays the current pump status information along with some Medtronic specific actions.
- **RileyLink Status**: The current status of the connection between your phone and Rileylink compatible device.  This should show as Connected at all times. Any other status may require user intervention. 
- **RileyLink Battery**: The current battery level of your EmaLink or OrangeLink device.  Dependent on selecting "Show battery level reported by OrangeLink/EmaLink/DiaLink device" in the Medtronic Pump Configuration menu.
- **Pump Status**: The current status of the pump connection.  As the pump will not be constantly connected this will primarily show the sleep icon.  There are a number of possible other status including "Waking Up" when AndroidAPS is trying to issue a command or other possible pump commands such as "Get Time", "Set TBR", etc. 
- **Battery**: Shows battery status based on the value chosen for Battery Type (Power View) in the Medtronic Pump Configuration menu.  
- **Last connection**: How long ago the last succesful pump connection happened.
- **Last Bolus**: How long ago the last succesful bolus was delivered.
- **Base Basal Rate**: This is the base basal rate that runs on pump at this hour in your active Profile.
- **Temp basal**: Temp basal currently being delivered which can be 0 units per hour.
- **Reservoir**: How much insulin is in reservoir (updated at least every hour).
- **Errors**: Error string if there is problem (mostly shows if there is error in configuration).

At the bottom of the screen there are three buttons:
- **Refresh** is for refreshing the current status of the pump. This should only be used if the connection was lost for a sustained period as this will require a full data refresh (retrieve history, get/set time, get profile, get battery status, etc).
- **Pump History**: Shows pump history (see [below](../Configuration/MedtronicPump#pump-history))
- **RL Stats**: Show RL Stats (see [below](../Configuration/MedtronicPump#rl-status-rileylink-status))

## Pump History
![Pump History Dialog](../images/Medtronic03.png)

Pump history is retrieved every 5 minutes and stored localy. Only the previous 24 hours worth of history is stored.  The allows for a convinient way to see pump behaviour should that be required.  The only items stored are those relevenant to AndroidAPS and will not inlcude a configuration function that has no relevance. 


## RL Status (RileyLink Status)
![RileyLink Status - Settings](../images/Medtronic04.png)
![RileyLink Status - History](../images/Medtronic05.png)


The RL Status dialog has two tabs:
- **Settings**: Shows settings about the RileyLink compatible device: Configured Address, Connected Device, Connection Status, Connection Error and RileyLink Firmware versions. Device Type is always Medtronic Pump, Model would be your model, Serial number is configured serial number, Pump Frequency shows which frequency you use, Last Frequency is last frequency used.
- **History**: Shows communication history, items with RileyLink shows state changes for RileyLink and Medtronic shows which commands were sent to pump.

## Actions
When the Medtronic driver is used, two additional actions are added to Actions Tab:
- **Wake and Tune Up** - In the event that AndroidAPS hasn't connected to your pump for a sustained period (it should connect every 5 minutes), you can force a Tune Up. This will try to contact your pump, by searching all of the possible radio frequencies used by your pump. In the event a succesful connection is made the succesful frequency will be set as the default. 
- **Reset RileyLink Config** - If you reset your RileyLink compatible device you may need to use this action so that device can be reconfigured (frequency set, frequency type set, encoding configured).


## Important notes

### OpenAPS users
OpenAPS users should note that AndroidAPS with Medtronic uses a completely different approach than OpenAPS.  Using AndroidAPS the primary method of interacting with th pump is via your phone.  In normal use cases it is likely that the only time it is required to use the pump menu is when changing resevoirs.  This is very different when using OpenAPS where at least some of a bolus is usually delivered via the quick bolus buttons.  In the event the pump is used to manually deliver a bolus there can be issues if AndroidAPS attempts to deliver one at the same time.  There are checks to try and prevent issues in such cases but this should still be avoided where possible.

### Logging
In the event you need to troubleshoot your Medtronic pump function select the menu icon in the upper left corner of the screen, select Maintainance and Log Settings. Options Pump, PumpComm, PumpBTComm need to be checked.

### Medtronic CGM
Medtronic CGM is currently NOT supported.

### Manual use of pump
You should avoid manually doing treatments things on your pump. All commands (bolus, TBR) should go through AndroidAPS, but if it happens that you will do manual commands, do NOT run commands with frequency less than 3 minutes (so if you do 2 boluses (for whatever reason), second should be started at least 3 minutes after first one).

## Timezone changes and DST (Daylight Saving Time) or Traveling with Medtronic Pump and AndroidAPS

Important thing to remember is that you should never disable loop when you are traveling (unless your CGMS can't do offline mode). AAPS will automatically detect Timezone changes and will send command to Pump to change time, when time on Phone is changed. 

Now if you travel to East and your TZ changes with adding hours (ex. from GMT+0 to GMT+2), pump history won't have problem and you don't have to worry... but if you travel to West and your TZ changes by removing hours (GMT+2 to GMT-0), then sychronization might be little iffy. In clear text, that means that for next x hours you will have to be careful, because your IOB, might be little weird. 

We are aware of this problem, and we are already looking into possible solution (see https://github.com/andyrozman/RileyLinkAAPS/issues/145), but for now, have that info in mind when traveling.



## FAQ

### Can I see the power of RileyLink/GNARL?
No. At the moment none of this devices support this and it probably won't even in the future.

### Is GNARL full replacement for RileyLink?
Yes. Author of GNARL added all functions used by Medtronic driver. All Medtronic communication is supported (at time of the writing (June/2019). GNARL can't be used for Omnipod communication. Downside of GNARL is that you have to build it yourself, and you have to have compatible version of hardware.

**Note from author:** Please note that the GNARL software is still experimental and lightly tested, and should not be considered as safe to use as a RileyLink.

### Where can I get RileyLink or GNARL?
Like mentioned before you can get devices here:
- RileyLink - You can get device here - [getrileylink.org](https://getrileylink.org/).
- GNARL - You can get info here, but device needs to be ordered elsewhere ([github.com/ecc1/gnarl](https://github.com/ecc1/gnarl)).

### What to do if I loose connection to RileyLink and/or pump?
1. Run "Wake Up and Tune" action, this will try to find right frequency to communicate with pump.
2. Disable Bluetooth, wait 10s and enable it again. This will force reconnecting to RileyLink.
3. Reset RileyLink, after you do that do not forget to run "Reset RileyLink Config" action.
4. Try 3 and 2 together.
5. Reset RileyLink and reset phone.

### How to determine what Frequency my pump uses
![Pump Model](../images/Medtronic06.png)

If you turn your pump around in first line on right side you will see special 3 letter code. First two letters determine frequency type and last one determines color. Here are possible values for Frequency:
- NA - North America (in frequency selection you need to select "US & Canada (916 MHz)")
- CA - Canada (in frequency selection you need to select "US & Canada (916 MHz)")
- WW - Worldwide (in frequency selection you need to select "Worldwide (868 Mhz)")
