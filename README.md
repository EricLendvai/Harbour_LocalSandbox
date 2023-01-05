# Harbour_LocalSandbox
The Harbour_LocalSandbox is used to test/learn Harbour.   
This version also includes the Harbour_VFP and Harbour_ORM libraries

View [ChangeLog.md](ChangeLog.md) for list of enhancements and fixes.

# VS Code Devcontainer
- In order to develop in any environement you can use the VS Code devcontainer provided in this repo.   
- Install remote containers extension: https://aka.ms/vscode-remote/download/containers   
- WILL NOT BE ABLE TO COMPILE IN DEBUG MODE, due to LoadAllHarbourAPI_linux.prg (probably an issue with default Harbour debugger.)   
- Due to a bug in VSCode mounted volumes, not handling file and record locs, the table created and used must be created inside the container, and thus are volatite (will not be saved on container rebuild).
