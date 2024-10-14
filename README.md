# slicer-cli-example
An example for creating a DSA slicer-cli.

## Instructions
\* Tip: be logged in as an admin user when working in the DSA for this.

The CLI is built using Docker: ```$ docker build -t <image-name>:<tag> .```

Your image can include one or more analysis that will be integrated in the HistomicsUI analysis panel and have an API created for it. To add custom CLIs follow the examples shown:
* cli/PositivePixelCount/
    - This is a modified version of the PositivePixelCount CLI that is included in the base installation of the DSA.


To add new CLI:
1. Modify the "slicer_cli_list.json" file to include your new CLI:
    - For example: ```"CustomAnalysis": {"type": "python"}```.
2. Creata new directory in the "cli" directory, for example: ```CustomAnalysis/```.
3. In your new directory add a Python and an XML file of the same name as the directory (```CustomAnalysis.py, CustomAnalysis.xml```).
4. Follow the examples for defining the XML file, and modify the parameters section as needed.
5. The Python file is where your analysis should go, note that it uses CLI parse class that is unique to the DSA, which allows reading parameters appropriately (such as the filepath to the WSI you are analyzing). The name of the parameters in the parser are defined in the XML file, so look at both these files when creating the CLI.

### Adding the CLI to your DSA instance.
1. All DSA instances contain a "Tasks" collection, navigate into this collection and then in the "Slicer CLI Web Tasks" folder.
2. In this folder there will be a button at the top with the word "CLI", clicking this button will open up a pop menu for uploading new CLI Docker images.
3. Input your Docker image to upload to the DSA instance, i.e. ```<image-name>:<tag>```.
    - NOTE: If you are developing, it is recommended to build your Docker image in the same machine running the DSA instance and that you only have one worker handling DSA tasks. If this is not the case you will have to push your new Docker image to Docker Hub first so the DSA instance and workers can pull it (this takes considerable more time!).
    - You can use the admin job menu to see if your upload was successful or if it failed, inspect why.
4. You should be able to see your new CLI as an anlysis in the HistomicsUI viewer and also in the DSA API page.