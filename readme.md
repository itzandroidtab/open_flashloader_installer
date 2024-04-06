# Open flash loader installer (for SEGGER J-Link)
This project allows you to create a custom installer for your open flash loader in 4 steps. This allows you to distribute a custom installer that automaticly installs the flash loaders in the correct location without user intervention.

## Prerequisites
* Windows (for now)
* Visual studio
* The [Microsoft Visual Studio Installer Projects](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2022InstallerProjects) plugin
* J-link >= V7.80
* Open flash loader executable

## How to create a device xml file
SEGGER J-Link uses xml files to add support for external loaders. The xml file configures the follwing:
* The target Microcontroller for the loader
* The address the memory is located
* What executable file to load
* The name it shows up as in the J-Link software

Example xml file for the LPC1756 is25lq040b open flash loader.
```xml
<DataBase>
    <Device>
        <ChipInfo Vendor="NXP" Name="LPC1756" />
        <FlashBankInfo Name="NOR Flash" BaseAddr="0xA0000000">
            <LoaderInfo Name="SPI flash loader" MaxSize="0x01000000" Loader="flash_loader.elf" LoaderType="FLASH_ALGO_TYPE_OPEN" />
        </FlashBankInfo>
    </Device>
</DataBase>
```

More info can be found at https://wiki.segger.com/J-Link_Device_Support_Kit

## How to use
How to configure the project to include your open flash loaders

1. Open the visual studio project. (The project should open on the "File System" page. If it does not right click on the project name and "view" -> "File System")
2. Right click "Application Folder" -> "Add" -> "File"
3. Repeat step 2 for as many files as you want to add (make sure to at least add one xml file)
4. Build project

Optional steps if you want to change the manufacturer and productname (these steps should be done before building):
1. Click on the project name
2. Change the Author, Manufacturer, URl, productName in the properties