# **RS-SWANe Installation & Maintenance Guide**  

This guide provides step-by-step instructions to install Python3, dcm2niix, FSL, FreeSurfer, 3D Slicer, Graphviz, and SWANe on Ubuntu.  

## **1. Install Python3**  
### **Installation**  
Ensure Python3 is installed and up-to-date:  
```bash
sudo apt update
sudo apt install python3 python3-pip
```  

### **Verify Installation**  
```bash
python3 --version
pip3 --version
```  

### **Maintenance**  
- Update Python packages:  
   ```bash
   pip3 install --upgrade pip
   pip3 list --outdated | cut -d' ' -f1 | xargs -n1 pip3 install --upgrade
   ```  

## **2. Install dcm2niix**  
### **Installation**  
1. Via `apt`:  
   ```bash
   sudo apt update
   sudo apt install dcm2niix
   ```  
2. Alternatively, build from source:  
   ```bash
   git clone https://github.com/rordenlab/dcm2niix.git
   cd dcm2niix/console
   mkdir build && cd build
   cmake ..
   make
   sudo make install
   ```  

### **Verify Installation**  
```bash
dcm2niix --version
```  

### **Maintenance**  
To update, repeat source installation steps.  

## **3. Install FSL**  
### **Installation**  
1. Download and install the FSL installer:  
   ```bash
   wget https://fsl.fmrib.ox.ac.uk/fsldownloads/fslinstaller.py
   python3 fslinstaller.py
   ```  

2. Add to `~/.bashrc`:  
   ```bash
   export FSLDIR=/usr/local/fsl
   . ${FSLDIR}/etc/fslconf/fsl.sh
   export PATH=${FSLDIR}/bin:$PATH
   ```  

3. Reload the shell:  
   ```bash
   source ~/.bashrc
   ```  

### **Verify Installation**  
```bash
flirt -version
```  

### **Maintenance**  
Run the installer script to update:  
```bash
python3 fslinstaller.py
```  

## **4. Install FreeSurfer**  
### **Installation**  
1. Download the software from [FreeSurfer's Website](https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall).  

2. Extract and move it:  
   ```bash
   tar -xvzf freesurfer-Linux-<version>.tar.gz
   sudo mv freesurfer /usr/local/
   sudo chmod -R 755 /usr/local/freesurfer
   ```  

3. Add to `~/.bashrc`:  
   ```bash
   export FREESURFER_HOME=/usr/local/freesurfer
   source $FREESURFER_HOME/SetUpFreeSurfer.sh
   ```  

4. Register for a license at [this link](https://surfer.nmr.mgh.harvard.edu/fswiki/License), and copy `license.txt`:  
   ```bash
   cp /path/to/license.txt /usr/local/freesurfer/
   ```  

5. Reload the shell:  
   ```bash
   source ~/.bashrc
   ```  

### **Verify Installation**  
```bash
recon-all -version
```  

### **Maintenance**  
Reinstall the latest version when required.  

## **5. Install 3D Slicer**  
### **Installation**  
1. Download the latest release from [3D Slicer's website](https://www.slicer.org/).  

2. Extract and move it:  
   ```bash
   tar -xvzf Slicer-<version>-linux-amd64.tar.gz
   sudo mv Slicer-<version> /opt/slicer
   ```  

3. Add to `PATH` in `~/.bashrc`:  
   ```bash
   export PATH=/opt/slicer/Slicer-<version>:$PATH
   ```  

4. Reload the shell:  
   ```bash
   source ~/.bashrc
   ```  

### **Install SlicerFreeSurfer Extension**  
1. Open Slicer, navigate to **Extensions Manager**.  
2. Search for "SlicerFreeSurfer" and install it.  

## **6. Install Graphviz**  
### **Installation**  
```bash
sudo apt update
sudo apt install graphviz
```  

### **Verify Installation**  
```bash
dot -version
```  

## **7. Install and Run SWANe**  
### **Installation**  
1. Create a virtual environment:  
   ```bash
   python3 -m venv swane_env
   ```  

2. Activate the virtual environment:  
   ```bash
   source swane_env/bin/activate
   ```  

3. Install SWANe:  
   ```bash
   pip install swane
   ```  

4. Run SWANe:  
   ```bash
   python3 -m swane
   ```  

5. Exit the virtual environment:  
   ```bash
   deactivate
   ```  

## **8. Configuration Recap**  
Ensure your `~/.bashrc` includes the following environment variables:  
```bash
# FreeSurfer
export FREESURFER_HOME=/usr/local/freesurfer
source $FREESURFER_HOME/SetUpFreeSurfer.sh

# FSL
export FSLDIR=/usr/local/fsl
. ${FSLDIR}/etc/fslconf/fsl.sh
export PATH=${FSLDIR}/bin:$PATH

# Slicer
export PATH=/opt/slicer/Slicer-<version>:$PATH
```  

Reload the shell:  
```bash
source ~/.bashrc
```  

## **9. Maintenance**  
1. **Update Tools**  
   Regularly visit the official websites for updates.  

2. **Backup Configurations**  
   Save `~/.bashrc` and `license.txt` for FreeSurfer.  

3. **Test Environment**  
   Periodically check installations:  
   ```bash
   which python3
   which dcm2niix
   which flirt
   which recon-all
   which dot
   ```  

4. **System Updates**  
   Keep your system up-to-date:  
   ```bash
   sudo apt update && sudo apt upgrade
   ```  
