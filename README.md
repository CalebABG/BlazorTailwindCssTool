# Blazor TailWind CSS Tool

## Handy tool to generate the latest Tailwind CSS using Docker for your Blazor project.

### Helpful Links

1. [TailWind Css Docs](https://tailwindcss.com/docs)
2. [TailWind Css Installation](https://tailwindcss.com/docs/installation#customizing-your-configuration)
3. [Docker](https://www.docker.com/get-started)
4. [Node Js](https://nodejs.org/en/)

## How to Use (Please Read :)

### Breakdown

This tool uses ```Docker``` as a, no pun intended, *container* for bundling up a ```Node JS``` environment which has installed TailWind CSS's Npx Cli tool to build your css file!

To make use of this tool, for now, you'll need to drop the ```Dockerfile.cssbuild``` and ```cssbuild.sh``` files into the root directory of your Blazor project
   - Don't worry, these files are **NOT** harmful and **DON'T** gather any data about your project.
   - Both files make use of the Blazor project so it can find the TailWind CSS's config file, as well as the master css file for the project.

The ```Styles``` folder is purely a structural housing for the master css file as well as the config file. If you'd like or if your project has different locations where the config file (if you have one, as it's optional), as well as the css file, you can change the path to them in the ```cssbuild.sh``` file.

The ```cssbuild.sh``` file is where you can change the where the path for the master css file, the config file, and where you want the built TailWind CSS file to be placed.

- **Note:** All paths for files locations are relative to where the Docker container is run from
  - Ex. Blazor app root is: ```TestBlazorApp\```, and the folder for style resources is: ```TestBlazorApp\Styles```
  - Then, in the ```cssbuild.sh```
    - ```
      ./Styles/site.css == TestBlazorApp\Styles\site.css
      ```
  
- The **first** argument to the npx cli tool is the path to the master css file
  - Default path: ```./Styles/site.css```

- The **second** argument is the output path for the built TailWind CSS file. I.e, where in the Blazor project do you want to file placed
  - Default path: ```./wwwroot/css/site.css```

- The **third** and *optional* argument is the config for the npx cli tool. In the config you can set whether you want the file to be built for dev or production environment (production file is **way** smaller in size)
  - Default path: ```./Styles/tailwind.config.js```


### Tool Commands

Now that you understand the how, lets get to the GO! 

**Note:** Make sure you're in the root of your Blazor project before executing the following commands! Also, for all intents and purposes, the image name the commands use is: ```testapp```, but you can name the image anything you want.

1. Building the Docker image:
   1. ```
      docker build --no-cache -f Dockerfile.cssbuild -t testapp/tailwindcssbuild .
      ```
2. Running the Docker image:
   1. ```
      docker run -it --rm --name test-twcbuild -e NODE_ENV=development -v ${PWD}:/app testapp/tailwindcssbuild
      ```
    - **Note:** Here, you can change the ```NODE_ENV``` to either dev or prod if needed

3. Removing the Docker image:
   1. ```
      docker image rm testapp/tailwindcssbuild
      ```

