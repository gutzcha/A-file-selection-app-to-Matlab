# file_slection_app_for_matlab
Integrate the file selection app into any Matlab app
or use this app as a stand-alone file selector and export the data to the workspace.

## Installation:
* Download and unzip the file
* Add app folder to Matlab path

## Getting started:
### Stand alone app:
You can use the app as a stand-alone app as a file selector:
Pass the command:
```
FileSelectorApp
```
If Matlab doesn't recognize the function (Unrecognized function or variable 'FileSelectorApp'.), 
then make sure that you added the app to the Matlab path
* https://uk.mathworks.com/help/matlab/ref/addpath.html

### Integrate app into other apps:
1. Open the app into which you wish to integrate the FileSelectorApp with the app designer 
2. Add a public property
  ![image](https://user-images.githubusercontent.com/35958758/168674410-d24d3fbf-138d-4c7a-9e58-5e9e75f82981.png)
3. Past the next line in place of the new property
This new property has three fields:
a. file_list : table with two columns - filenames and variableind (which hold the index of a specific variable, relevant for mat files)
b. valid_flag: boolean - true if the app successfully loaded files
c. last_source_folder: char - the path to the last loaded folder so that next time it will load that folder automatically
![image](https://user-images.githubusercontent.com/35958758/168674714-b3b1d4b3-9796-4f85-abf4-731bc6fddc79.png)

```
 app_output = struct('file_list',[],'valid_flag',false, 'last_source_folder','') % Connect handle to outer app here 
```


4. Add a function (private or public), and copy-past the next lines:
![image](https://user-images.githubusercontent.com/35958758/168675099-3457f944-a057-4122-a686-4718d8ed3405.png)


```
h = FileSelectorApp(app); 
waitfor(h); % This will freeze you app until the FileSelectorApp is closed
% Debug
%    disp(app.file_selector)
```
Uncomment the last line to debug or display the values.

5. The property app_output will hold a table with the selected file paths

## How to use
![image](https://user-images.githubusercontent.com/35958758/168677963-dd26d8cc-8a29-4cd5-a2b3-897b001beff4.png)
#### A. Filter parameters:
1. "Matfile" StateButton and "Class name" field: 
If  "Matfile" StateButton "On," then the app will load only the matfile that contains a variable of the class in the "Class name" field (double if empty).
Here is where the 'variableind' variable in the 'file_list' table in the 'app_output' property is useful; it indicates the index of the variable in the matfile
(the first one if there is more than one)
2. "Search filter": 
Add a search filter to refine the loaded file, for example, "*.wav" to load only wav files or "*June*" to load the only files that contain the word "June."
#### B. Load files
1. "Select folder" button: Open folder selection UI and load files from the folder
2. "Include subfolder" StateButton: If "On" the extended search to subfolder as well, (effectively adds "**\\" to the search filter) 
3. "Refresh folder" button: Reload the folder
#### C. Select files
The loaded files will be shown in the left table, select any number of files and transfer them to the select list on the right
#### D. Export file list
If the app was initiated as a stand-alone app, this action exports the table to the workspace and closes the app.
If the app was initiated as an integrated element in another app, this action will update the app.app_output handle and close the app.


[![View File slection app for Matlab on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://uk.mathworks.com/matlabcentral/fileexchange/111675-file-slection-app-for-matlab)

