### What I inherited from Bob Bruccoleri (Bash) vs. what I developed (Python)

Left: I inherited a Bash process from Bob. ~100 files in one directory. I had to modify the scripts, run, debug, etc.. The Dockerfile disappeared if the step succeeded. The code and process were one. I asked Bob about rewriting. He told me to wait, so I did.
Middle: There was no Python anything at the end of my first update, no folders, no scripts generating other scripts etc.
Right: I did what they are claiming as theirs. It was my idea.
<table>
  <th>What I inherit in August 2022</th>
    <th>11/22 - end of my first update</t>
    <th>11/22 - I start rewriting</t>
</th>
  <tr>
  <td align="center">
<img width="47%" src="https://github.com/user-attachments/assets/0576d007-75a9-46a2-9a59-88d339095b0e"/> <img width="45%" src="https://github.com/user-attachments/assets/89b227c6-5da2-4b1b-8e2e-d8f7d534b01c"/>
  </td>
  <td align="center">
    <img src="https://github.com/user-attachments/assets/5add5486-a88d-4ae5-b425-1f316f85c571"/>
  </td>
  <td align="center">
    <img width="95%" src="https://github.com/user-attachments/assets/97dd9208-00a1-4e93-869f-59ce216abd4c"/>z
  </td>

</tr></table>

![image](https://github.com/user-attachments/assets/c2a07692-95a8-4b1a-bd94-82e561e982f6)

### What's up with Andrew Smith avoiding interactions and plagiarizing?

My old boss roped Andrew Smith and Isaac Neuhaus into helping Brian Rini, the guy who runs [this trial](https://www.clinicaltrials.gov/study/NCT05361720) and wrote "genetic testing" about RNA, didn't mention the Department of Defense until two years into the trial, and used a fictitious identifier. I didn't know. I only looked because the separation agreement reeked of despair (and stupidity).

<kbd><img width=555 src="https://github.com/user-attachments/assets/481dd48b-471c-43be-8f57-1c129f428587" /> </kbd>

### Request for additional work on my old code, for free and without attribution

In February, my former employer emails me.  She fired me because I wouldn't violate FDA regulations, and had no involvement in this at all. I'm an author and have access to the code, and I somehow know what it's about. Note the branch. This is called "signaling intent".

<kbd><img width=555 src="https://github.com/user-attachments/assets/e312e559-2dc4-41d8-9e1a-9ad34ee16746" /> </kbd>

I'm a middle author. Sarah and Eric are included. Hell, no.

<kbd><img width=555 src="https://github.com/user-attachments/assets/fde1ae3a-d5bf-4f56-8cb7-39479fa606d8" /> </kbd>

Andrew knows it's my code, but doesn't reply. They wanted me to write about my old code, after committing me to BMS and an ex-BMS client at the same time.

<kbd><img width=555 src="https://github.com/user-attachments/assets/bf8360c6-c513-44d3-b0f8-94bfc37bc9bf" /> </kbd>

On 4/25, he drops me from the group:

<kbd><img width=555 src="https://github.com/user-attachments/assets/946955e8-3c8e-41ab-aece-348538318b04" /> </kbd>

On 4/28, they submit the manuscript without me, and the branch is gone. There's a vague acknowledgment, but this is my work and my ideas.

<kbd><img width=555 src="https://github.com/user-attachments/assets/42ffacfb-83d1-40f5-a185-11d7c3f08562" /> </kbd>

Everything below is from my fork on 4/25, after Andrew dropped me from the group.

---
# DockerImageBuilder

The DockerImageBuilder is a powerful, layered approach to building complex Docker images that's ideal for computational research teams. The system breaks down the build process into discrete stages using configuration files and bash scripts, providing several key advantages:

* Efficient caching between builds
* Easy debugging at each stage
* Modular component assembly
* In-container source code compilation
* External code mounting support to reduce image size

The entire build process is captured in version-controlled configuration files, making it straightforward to reconstruct and update images as requirements evolve.

## Build a basic image

1. Clone this repository & move into the directory:

  ```bash
    git clone https://github.com/TBIO-RR-Group/DockerImageBuilder.git
    cd DockerImageBuilder
  ```

2. Set up the appropriate environment. You may use your choice of package/environment manager. Here we will show how to create the appropriate environment using mamba.

  ```bash
     mamba env create -f environment.yml
     mamba activate DockerImageBuilder
  ```

3. Create the image builder script. 
 
  ```bash
     bash generate_build.sh
  ```

4. Build the image. Must use sudo privileges to create appropriate base directories. This process takes approximately an hour depending on your system.

  ```bash
     sudo bash go_build.sh
  ```

5. Sync appropriate files to image.

  ```bash
    sudo build_self_contained_image.sh
  ```

## Recommendations for building a custom image.

* The default image has the following specifications:
  * base image - Ubuntu 22.04
  * python v3.10.6
  * R v4.4.2
  * IDEs - RStudio, Jupyter, JupyterLab, Visual Studio Code

* The user can change the base image of the build by editing the value assigned to `current_image` in `build_scripts/generate_master_build_script.sh`.
* The user can set which python version is used by editing `PYTHON_VERSION` in `config_files/setup.sh`. This image has been tested with v2.7.18, v3.8.12, v3.9.10, or v3.10.2. It is also possible to install multiple versions of Python.
* The user may need to specify the python3 path in `build_self_contained_image.sh`, depending on their setup.
* To update the R version, the user needs to update `R_version` in `setup.sh`.
* To change the R packages installed in the image, the user should edit `config_files/R_packages/rpkgs.txt`.
* The user can add their software of choice by adding a new step in `build_scripts/generate_master_build_script.sh`.
* The user can update the variables in `setup.sh` & `build_setup.sh` to change other parameters of the build.
* The user can control which steps in the build run (or don't run) by editing `build_scripts/generate_master_build_script.sh`.
* Some scripts exist in the repo but are unused to show how different software/packages could potentially be installed. These can be found in `build_scripts/efs` with the prefix BUILD_*.

## Dependencies

* Docker
* python3
