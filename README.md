# Usefull links and tutorials
### Epic tutorials and links
* [EPIC Landing Page](https://eic.github.io/documentation/landingpage.html)
* [Tutorial: Setting Up EIC Environment](https://eic.github.io/tutorial-setting-up-environment/02-eic-shell/index.html)
  
* Main web page of EPIC experiment : https://wiki.bnl.gov/EPIC
* Indico Set of Tutorials about EPIC (https://indico.bnl.gov/category/443/)
* [Quick start tutorial on ATHENA detector design and simulation](https://eic.phy.anl.gov/tutorials/eic_tutorial/getting-started/quickstart)


### Programming tutorials
* [HEP Essentials C++ course presentation](https://indico.cern.ch/event/1266661/attachments/2711308/4694049/Essentials.pdf) + video (https://indico.cern.ch/event/1266661/)
* [A ROOT Guide For Beginners](https://root.cern.ch/root/htmldoc/guides/primer/ROOTPrimer.html)
* [Git one page guide](https://rogerdudler.github.io/git-guide/index.html)
* [Scientific computing resources](https://hepsoftwarefoundation.org/training/center.html)




### Physics literature

  1. A. Accardi   et al.,“Electron-Ion Collider: The next QCD frontier: Understanding the glue that binds us all", Eur. Phys. J. A (2016) 52: 268. https://link.springer.com/content/pdf/10.1140/epja/i2016-16268-9.pdf
  2. Ch. Wood and M. Sherman,“Inside the Proton, the ‘Most Complicated Thing You Could Possibly Imagine“,  Quantamagazine, October 19, 2022.https://www.quantamagazine.org/inside-the-proton-the-most-complicated-thing-imaginable-20221019/
  3. R. A. Khalek et al., “Science Requirements and Detector Concepts for the Electron-Ion Collider: EIC Yellow Report, Nucl. Phys. A 1026 (2022) 122447.https://doi.org/10.1016/j.nuclphysa.2022.122447
  4. M. Livan and  R. Wigmans, “Calorimetry for Collider Physics, an Introduction“, ISBN 978-3-030-23652-6, Springer Nature Switzerland AG 2019.
  5. B. Povh et al., Particles and Nuclei, An Introduction to Physical Concepts, ISBN: 978-3-640-79367-0,  Springer 2008.
https://eprints.ukh.ac.id/id/eprint/207/1/2015_Book_ParticlesAndNuclei.pdf



---



## Install on Windows

Visual Studio Code https://code.visualstudio.com/download

Docker https://docs.docker.com/desktop/install/windows-install/

apply integration to wsl2:

![image](https://github.com/aprozo/SetupWSL/assets/33087030/21f471b8-709c-40fe-9869-0b5d90cef718)


NoMachine https://www.nomachine.com/


### VS code extensions:
``` bash
code --install-extension albertopdrf.root-file-viewer 
code --install-extension eamodio.gitlens
code --install-extension esbenp.prettier-vscode
code --install-extension GitHub.copilot
code --install-extension James-Yu.latex-workshop
code --install-extension ms-azuretools.vscode-docker
code --install-extension MS-CEINTL.vscode-language-pack-ru
code --install-extension ms-vscode.cmake-tools
code --install-extension ms-vscode.cpptools
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension ms-vscode.cpptools-themes
code --install-extension twxs.cmake
```

## Install on WSL
open Windows PowerShell as admin
`wsl --install`  - it will install latest Ubuntu version

reboot

start new UBUNTU terminal, and update some packages:

``` bash
cd ~
sudo apt-get install dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev \
libxft-dev libxext-dev python3 libssl-dev \ 
gfortran libpcre3-dev \
xlibmesa-glu-dev libglew-dev libftgl-dev \
libmysqlclient-dev libfftw3-dev libcfitsio-dev \
graphviz-dev libavahi-compat-libdnssd-dev \
libldap2-dev python3-dev libxml2-dev libkrb5-dev \
libgsl0-dev qtwebengine5-dev -y 

 mkdir install 
 cd install 
 wget https://root.cern/download/root_v6.28.04.Linux-ubuntu22-x86_64-gcc11.3.tar.gz 
 tar -xzvf root_v6.28.04.Linux-ubuntu22-x86_64-gcc11.3.tar.gz 
 rm root_v6.28.04.Linux-ubuntu22-x86_64-gcc11.3.tar.gz 
 source ~/install/root/bin/thisroot.sh
 
 sudo apt-get install firefox xdg-utils sshfs -y 
 sudo apt-get install texlive-full -y
 sudo apt-get install python3-pip
 pip install notebook
 export PATH="$HOME/.local/bin:$PATH"
```

### EIC specific

# Download docker container:
``` bash
docker pull eicweb/jug_xl:nightly
docker run -itv /home/prozorov/eic:/home/prozorov/eic eicweb/jug_xl:nightly
cd /home/prozorov/eic/ && git clone https://github.com/eic/epic.git
```

Now, one can start Docker service via Windows Desktop and run previous container (all changes will be saved in this particular container) 
![image](https://github.com/aprozo/SetupWSL/assets/33087030/2f8176f8-dbe2-4304-afb1-ca814d60778c)

# Run in VS Code:
to open VS Code within a running container:

After starting a container, run ``` code .``` anywhere on WSL2

Then `Ctrl + P` , start typing:

`>Dev Containers: Attach to a Running Container`, and attach it to the new container

Now VS Code is opened in a container.


# Helpful features for VS Code programming:
Include paths on docker for .vscode config file for all eic libraries:

"/usr/local/include/**",

"/opt/software/linux-debian-x86_64_v2/gcc-12.2.0/root-6.26.10-ypxsyrtxgzrojuy7ainximgo4er5zmmz/include"

in project folder create `.vscode/c_cpp_properties.json` with the following lines:

```cpp 
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/local/include/**",
                "/opt/software/linux-debian-x86_64_v2/gcc-12.2.0/root-6.26.10-ypxsyrtxgzrojuy7ainximgo4er5zmmz/include/**"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c17",
            "cppStandard": "c++14",
            "intelliSenseMode": "linux-clang-x64",
            "compileCommands": "${workspaceFolder}/epic/build/compile_commands.json"
        }
    ],
    "version": 4
}
```



## EPIC geometry run: 
use the following commands and create a `run.sh` file in the `../eic/epic/` to fastly run everything:
```bash
cmake -B build -S . -DCMAKE_INSTALL_PREFIX=install
cmake --build build -- install -j4
source install/setup.sh
dd_web_display --export $DETECTOR_PATH/epic_calorimeters.xml
```
