# Options
## Setup Parameters and Their Roles
Your answers will generate a project based on your input values, below you can find the variables with their description and implications  

### `setup_mode`
Defines the overall setup approach for your environment. tweak the customization you want during server and Docker environment creation.

- **Basic**: minmal prompts. you will be asked to input your project name ([`project_name`](#project_name)), remote repository link ([`repo_url`](#repo_url)) and framework of your choice ([`ml_framework`](#ml_framework)) it recommend defaults for most options.

- **Advanced**: Lets you control Compute site ([chameleon_site](#chameleon_site)), GPU type ([`gpu_type`](#gpu_type)), CUDA version ([`cuda_version`](#cuda_version)), storage site ([`bucket_site`](#bucket_site))
The rest of the documentation shows what these options are and their implications 
- **Type**: `single-select`
- **Default**: `Basic`

--- 

### `project_name`

- We recommend setting `project name` as the prefix for the lease name 
- It is used everywhere your project is referenced:   
    - created buckets (e.g., `project-name-data`, `project-name-mlflow-artifacts`)
    - Compute instances /servers are going to include the `project_name` as their prefix 
    
        ```python
            # when creating a server
			s = server.Server(
			f"{{ project_name }}-node-{username}"
        ```
			  
	- Your material on the compute instance will be under a directory named after your `project_name`
    - The containerized environment will look for a directory with the `project_name` directory 
	- most commands and scripts assume a unified `project_name`
- **Rules**: only letters, numbers, hyphen (-), and underscore (_). no spaces.
- **Tip**: Choose something short and memorable — remember this will show up in multiple commands and URLs
- **Type:** `str`

---

### `repo_url`

- The remote Git repository where the generated project will live, we recommend creating a remote repository (e.g [GitHub](github.com) or [GitLab](gitlab.com)). 
- Accepts HTTPS or SSH URLs (e.g., `https://github.com/user/repo.git` or `git@gitlab.com:user/repo.git`).
- After having your project generated, you need to push the code there. (see [Github](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github) / [Gitlab](https://forum.gitlab.com/t/how-do-i-push-a-project-to-a-newly-created-git-repo-on-gitlab/68426) Guide on pushing code to remote repo)
- **Type:** `str`
- **Note**: can accept blank if you need to set the repository later,
you will need to [manully input](reference_later) the remote repo in create_server notebook. 

---

### `chameleon_site`
###### *work only under advanced*
The site where your leases at, and compute resources will be provisioned. 
- This doesn’t control persistent storage storage location (that’s [`bucket_site`](#bucket_site)).
#### **options**
- CHI@TACC → Most GPU bare metal nodes.
- CHI@UC → University of Chicago resources.
- KVM@TACC → VM(Virtual Machines )-based compute at TACC.
- **Type:** `select`
- **Default**: `CHI@TACC`

--- 

### `bucket_site`
###### *work only under advanced*

- This is where your [object storage contrainers](https://chameleoncloud.readthedocs.io/en/latest/technical/swift/index.html#object-store) for you project will live.
#### **options**

- CHI@TACC: Texas Advanced Computing Center
- CHI@UC: University of Chicago
- **auto** is usually the best choice unless you have a reason to store data in a specific location. it matches your selected `chameleon_site` if object storage containers are available, if not it defaults to CHI@TACC site. 
- **Type:** `select`
- **Default**: `CHI@TACC`

--- 

### `gpu_type`
###### *work only under advanced*

- The type of GPU (or CPU-only) node you want to create and configure. this assumes that you have reserved a node and you know which type it is AMD, NVIDIA or CPU.
- configuring a server from a lease require the `gpu_type`, as different `gpus` have different setup process. 
- `nvidia` and `amd` require different container images to. so your decision will result in selecting the appropriate [container images](https://github.com/A7med7x7/Chameo/tree/dev/template/docker)
- **Type:** `multi-choice` - you can select multiple types. 
- **Default**: `NVIDIA`
- **Note**: when selecting `chemeleon_site` = KVM@TACC the GPU flavors run on NVIDIA hardware as there are no AMD variant. 

---  

### `ml_framework`

- Selects the primary ML/deep learning framework for your environment.
- It will decide which container image to include and use for your Jupyter Lab. 
- Custom training code for the selected `ml_framework` will be generated
- **pytorch** – Flexible, widely used deep learning library. Supports CUDA (NVIDIA) and ROCm (AMD).
- **pytorch-lightning** – High-level wrapper for PyTorch that simplifies training loops. Supports CUDA (NVIDIA) and ROCm (AMD).
- **tensorflow** – Popular deep learning library with a strong ecosystem. 
- **scikit-learn** –  Machine Learning and data science stack (pandas, scikit-learn, matplotlib, etc.) without deep learning frameworks.
- **Note**: _PyTorch_ and _PyTorch Lightning_ will prompt for CUDA/ROCm version if you select GPU types.
- **Type** `multi-choice`: you can select multiple frameworks. 

---

### `cuda_version` 
###### *work only under advanced and GPU == NVIDIA*

- Choose the CUDA version that matches your code and driver requirements.
    - `cuda11-latest` : highly compatible with most GPUs in Chameleon Cloud 
    - `cuda12-latest` : The latest version designed to work with newer GPU architectures
- **Type** `select`
- **Default**: `cuda11-latest`
---
### `env_setup_mode`
###### *work only under advanced* 
How would you like to configure your server (.env file generation & docker compose setup)?
You have two options:
- **SSH** : 
SSH into your reserved compute instance and follow the README instructions to generate the .env file and launch your docker compose environment.
- **Notebook**: 
stay inside Chameleon JupyterHub and use a notebook (2_configure_server.ipynb) provided in the chi directory to configure your server.
This approach is more guided and beginner-friendly.
- both methods generate the same .env file and launch the same docker compose environment.
The only difference is where you perform the steps: via SSH (manual control) or Notebook (fully browser-based).
- **Type**: `select`
- **Default**: `"notebook"` if `setup_mode == 'Basic'`

---

### `include_huggingface` 
###### *work only under advanced* 

If enabled, it configures the environment to include a HuggingFace token for seamless Hugging Face Hub access and caching of models/datasets . 
- During server setup you will be prompted to enter a [Hugging Face Token](https://huggingface.co/settings/tokens) 
- All models/datasets downloaded from Hugging Face will be stored on the mounted point `/mnt/data/`
- **Type**: `bool`
- **Default**: `true`_