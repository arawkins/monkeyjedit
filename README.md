# monkeyjedit
Some tools to add [Monkey language](http://monkey-x.com/) support to the [jEdit editor](http://jedit.org).

To install these tools, you'll need to locate the jEdit settings directory on your system (please see http://jedit.org/users-guide/settings-directory.html for details). The instructions below assume you've found your settings folder. These instructions also assume you have a working Monkey installation and are somewhat familiar with the Monkey build process (specifically the Trans compiler).

## Syntax highlighting
Syntax highlighting currently supports only the basic language (ie. Mojo keywords are not included). There is also some preliminary support for Monkey 2 keywords (Enum, Struct, etc...)

### Installation
1. Copy /modes/Monkey.xml into the /modes folder in your jEdit settings directory. 
2. In your jEdit settings directory, edit /modes/catalog and add the following line under `<MODES>`:
 

   `<MODE NAME="monkey" FILE="Monkey.xml" FILE_NAME_GLOB="*.monkey*" />`

You should now have monkey syntax highlighting! Check out http://jedit.org/users-guide/installing-modes.html for more details on installing and editing editing modes in jEdit.

## Transcc 
Also included here is a Commando script for the Console plugin that provides a simple GUI for running Trans. 

### Installation
1. Install the Console plugin in jEdit if you haven't already (Plugins -> Plugin Manager -> Install)
2. Copy /console/commando/transcc.xml into the /console/commando folder in your jEdit settings directory (create the folder if it doesn't exist).
3. In jEdit, look under Plugins->Console->Commands. You should see a transcc command. 
4. Optional: Bind a keyboard shortcut to this command. Open Utilities->Global Options->Shortcuts, put transcc in the filter box to find it, then choose a keyboard shortcut. You may also want to bind a keyboard shortcut to Plugin:Console:Run Last Command, which will allow you to quickly re-run transcc if it was the last command you ran with the console plugin.

### Usage
When you run the transcc command, you should get a small popup with the following options.

#### Path to transcc
Set the path to transcc on your system. It should be in the /bin folder in your Monkey installation directory. Make sure to choose the version for your OS (eg. transcc_linux on linux).

#### Target Monkey File
Set this to your main monkey file containing your Function Main(). If this is the first time you've run the command, it will auto-populate with the file in the current buffer (ie. the file you are editing).

#### Action
Set the action you want trans to take (Run, Build, Clean, or Update).

#### Target
Choose your target. This list is not dynamically generated. In other words, it may show targets that you don't have set up, and it may not show all of the targets you do have set up. If you edit the commando file (transcc.xml), you can add additional targets fairly easily by copying one of the OPTIONs in this area of the file:

        <CHOICE LABEL="Target" VARNAME="monkeyTarget"
           DEFAULT="Html5_Game">
           <OPTION LABEL="HTML5" VALUE="Html5_Game" />
           <OPTION LABEL="C++ Tool" VALUE="C++_Tool" />
           <OPTION LABEL="Flash" VALUE="Flash_Game" />
           <OPTION LABEL="Desktop (GLFW2)" VALUE="Desktop_Game_\(Glfw2\)" />
           <OPTION LABEL="Desktop (GLFW3)" VALUE="Desktop_Game_\(Glfw2\)" />
        </CHOICE>

Add a new <OPTION> with your target LABEL and VALUE. LABEL is what you'll see when running the command in jEdit, while VALUE is what will be passed to transcc. To see what targets you have available, try running the trans compiler from the command line. It will give you a list of your available targets.

#### Config
Choose between debug and release builds.

#### Optional: Modules folder
If you are storing your modules in another folder, you can enter that folder here. This should (in theory) override whatever is set up in your monkey config file.


