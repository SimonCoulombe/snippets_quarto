---
title: "Setting up text generation (llama3) and image generation (stable diffusion) on my windows 11 desktop with an old GPU Nvidia GTX1060 6GB VRAM"
description: |
  C'était vraiment plus facile que je pensais.
author: Simon Coulombe
date: 2024-04-20
categories: []
lang: en
image: "ollama_works_and_uses_gpu.png"
execute:
  echo: false
format:
  html:
    code-fold: false
#lightbox: true # to enable to for all figures in the document   https://quarto.org/docs/output-formats/html-lightbox-figures.html  
---




# Objective   

I want to setup those cool things on my desktop.   I'm curious if my 8-year old GPU can be of any use.  If it is, I might be motivated to upgrade my GPU.   



# Setup

  * Hardware:  Ryzen 5500 CPU, 32 GB de RAM, old-ass GTX1060 6GB GPU.    
  * Software: Windows 11 pro.  Up-to-date nvidia drivers.  Python 3.12 installed a while ago.     
  
  
note to self on how to get nvidia drivers:  Right-click on your desktop and select NVIDIA Control Panel. From the NVIDIA Control Panel menu, select Help \> System Information. )  
![](nvidiadrivers.png){.lightbox height="1.5in"}

#  Text generation:  running llama3 8B on Ollama  



Installation:    
  * Visit the [ollama github](https://github.com/ollama/ollama) page  
  * There is a link to a "windows preview" that will download "ollamasetup.exe".  Download it.  
  * Run `ollamasetup.exe`.  That's it. Wow.!

Running:  
go to the command prompt and type `ollama run llama3`.    
  
Notes:   
First I started using WSL, and other docker ideas, which was a bit more complicated.  I will leave the instructions at the bottom as an appendix. It worked, but more complicated than needed.

that's it.   

# Text to image:  running Stable Diffusion using "Stable Diffusion webui"      

Installation:   

  * Visit the [stable diffusion webui github](https://github.com/AUTOMATIC1111/stable-diffusion-webui) and follow the instructions for "Automatic Installation on Windows".  As of today, it reads like this:   

  * Install Python 3.10.6 (Newer version of Python does not support torch), checking "Add Python to PATH".  
  * Install git.  
  * `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git`    
  * Run `webui-user.bat`  as normal, non-administrator, user.  
  
  at first I had issues because I also had python 3.12 installed and would get errors.  Downloading python 3.10 and checking "adding python to path" solved it.  


Running:  
  * Run `webui-user.bat`  as normal, non-administrator, user.    

Notes:  
I tried a few approaches ( WSL, docker), but it turns out the easiest way is the obvious one.     

# Training a "LoRA" to get stablediffusion to create images of my friends.   

  * Visit the [koshua_ss github repo](https://github.com/bmaltais/kohya_ss) and follow the instructions to install the necessary dependencies ans setup windows.  As of today, they read like this:      
  
To install the necessary dependencies on a Windows system, follow these steps:

  * Install Python 3.10.11.  
      *During the installation process, ensure that you select the option to add Python to the 'PATH' environment variable.  
  * Install CUDA 11.8 toolkit.    
  * Install Git.   
  * Install the Visual Studio 2015, 2017, 2019, and 2022 redistributable.  

Setup Windows  
  
To set up the project, follow these steps:  

  * Open a terminal and navigate to the desired installation directory.  
  * Clone the repository by running the following command: `git clone https://github.com/bmaltais/kohya_ss.git`
  * Change into the kohya_ss directory:   `cd kohya_ss`
  * Run the setup script by executing the following command: `.\setup.bat `



During the accelerate config step, use the default values as proposed during the configuration unless you know your hardware demands otherwise. The amount of VRAM on your GPU does not impact the values used.  

Running:    

  * run `gui.bat`   
  * prepare 15 pictures at 512x512 resolution.   
      * I use paint to create square image (only keeep that person.  )
          * launch paint, load image  
          * press CTRL-A to select all image   
          * slide the part of the image you want to keep at the top-left of the canvas   
          * resize 1 dimension using the mouse   
          * file - properties - image size  ,  change the unchanged dimension  so that it matches the other one.   
          * {{< video how_resize_crop_image_to_square.mp4 >}}    
      * I used [birme.net](https://www.birme.net/) to resize all the square images to 512x512.  also, might as well rename them.  
  * caption the images with your keyword you want it to learn, this is done in koshya_ss, under "utilies" - "blip captioning". pick your poison between  [text instructions by Paulo Carvalho  (step 5 -  Prepare Dataset)](https://thepaulo.medium.com/generate-photos-of-yourself-by-training-a-lora-for-stable-diffusion-privately-on-aws-124463750ff5) or [video instructions by aitrepreneur]([https://www.youtube.com/watch?v=70H03cv57-o&t=253s)  
  * train the lora.  follow either [text instruction - step 6](https://thepaulo.medium.com/generate-photos-of-yourself-by-training-a-lora-for-stable-diffusion-privately-on-aws-124463750ff5) or keep watching the video instructions by aitrepreneur.  I appreciated the aitrepreneur instructiosn because they came with a [low vram koshya settings json ](LoraLowVRAMSettings.json) of settings I could use to configure the lora.  There was also a "normal vram" json.   
  * use your lora!  again, either follow Paulo's instructions at step7 or keep watching aitrepreneur's video.  
        
         

  
  
## troubleshooting koshya_ss   

make sure you have python 3.10. i think at some point i created a python 3.10 venv and activatd it before running ./setup.bat     
`py -3.10 -m venv venv`  
`.\venv\Scripts\activate`
`setup.bat`
  

# image to image - controlnet        

installed the controlnet extension  from the [Mikubill/sd-webui-controlnet](https://github.com/Mikubill/sd-webui-controlnet) github.




# Appendix:  using WSL to run Ollama

Au début, j'avais essayé WSL, mais ça semble pas nécessaire.  Je note quand même les étapes ici.   


J'ai installé WSL en suivant les [instructions sur le site de microsoft](https://learn.microsoft.com/en-us/windows/wsl/install). Simplement, tu ouvres le power shell en mode administrator puis tu tapes

``` powershell
wsl --install
wsl --update
```

Ensuite j'ai exécuté wsl et je me suis rendu compte que `nvidia-smi`, qui est nécessaire à l'utilisation du GPU par llama ne marchait pas.  C'est parce que j'avais déjà une autre version de wsl (celle de docker-desktop) et que c'était elle qui roulait par défaut.  J'ai changé la version par default et tout va mieux:

``` powershell  
wsl --list --verbose
wsl
nvidia-smi
exit
wsl --set-default ubuntu
wsl
nvidia-smi
exit

```
![](wsl-list-set-default.png){.lightbox height="1.5in"}

bon mon nvidia-smi marche.. alors pour installer ollama
(https://github.com/ollama/ollama?tab=readme-ov-file)
tout ce que j'ai à faire c'Est 
``` powershell    
wsl   
curl -fsSL https://ollama.com/install.sh | sh  
ollama run llama3    --verbose
```

et ça marche et ça utilise le GPU 
holy shit, c'était simple.

![](ollama_works_and_uses_gpu.png)


## References:    
  * https://learn.microsoft.com/en-us/windows/wsl/install  
  * https://github.com/ollama/ollama  
  * getting started with meta llama https://llama.meta.com/docs/get-started/  
  * todo: karpathy https://www.youtube.com/watch?v=kCc8FmEb1nY



## notes quarto pour un jour plus investiguer  

  * note quarto: lui semble avoir ce que je veux pour un code chunk, mais comment il fait? https://github.com/carpentries-incubator/reproducible-publications-quarto/blob/ad9a94a050ab8267125fc5b47a89bfbdf75a9670/\_episodes/02-quarto/05-code-qmd.md?plain=1#L121  
  * y'A meme un guide ici https://github.com/carpentries-incubator/reproducible-publications-quarto  
  *  carpentries template https://github.com/carpentries-incubator/template  
  * https://github.com/carpentries-incubator/reproducible-publications-quarto/blob/0a8b05ad9bc9219980378364aca281961f747a4a/_episodes_rmd/07-code-chunks.rmd  
  * slidecraft code quarto https://emilhvitfeldt.com/post/slidecraft-code-output/  

