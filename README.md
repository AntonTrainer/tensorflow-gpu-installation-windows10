# tensorflow-gpu-installation-windows10
## This is the process that I followed, after atempting many other methods, to install the GPU version of Tensorflow

**FIRST** 
Install Microsoft Visual Studio Community 2015 update 3 [from here](https://my.visualstudio.com/Downloads?q=visual%20studio%202015&wt.mc_id=o~msft~vscom~older-downloads) login or create account

You also need the Visual Studio 2015 SKD [from here](https://my.visualstudio.com/Downloads?q=visual%20studio%202015&wt.mc_id=o~msft~vscom~older-downloads) 

**SECOND**
Download CUDA **v9.0 (must be 9)** [here](https://developer.nvidia.com/cuda-90-download-archive) [following instructions](file:///C:/Program%20Files/NVIDIA%20GPU%20Computing%20Toolkit/CUDA/v10.0/doc/html/cuda-quick-start-guide/index.html)

#### Run the CUDA sample nbody (C:\ProgramData\NVIDIA Corporation\CUDA Samples\v9.0\5_Simulations\nbody)(nbody_vs2015.sln) 
Select "build solution" in VS, if it fails, select "retarget project" by right clicking on the project on the right side of the window, install the new skd when you are prompted to do so by VS, then rebuild the solution. 

Run the nbody application (C:\ProgramData\NVIDIA Corporation\CUDA Samples\v9.0\bin\win64\Debug), close

**THIRD**
Download cuDNN zipped folder and extract to "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0"

**FOURTH**
Add CUDA to path, this should also add the cuDNN files to the path because you extracted to the v9.0 folder, if not, see below. [from here](https://www.tensorflow.org/install/gpu)
	```SET PATH=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin;%PATH%
	SET PATH=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\extras\CUPTI\libx64;%PATH%
	SET PATH=C:\tools\cuda\bin;%PATH%```

If this doesn't work, follow these instructions - 
"""
The following steps describe how to build a cuDNN dependent program. In the following sections:

    your CUDA directory path is referred to as C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0
    your cuDNN directory path is referred to as <installpath>

    Navigate to your <installpath> directory containing cuDNN.
    Unzip the cuDNN package.

    cudnn-9.0-windows7-x64-v7.zip

    or

    cudnn-9.0-windows10-x64-v7.zip

    Copy the following files into the CUDA Toolkit directory.
        Copy <installpath>\cuda\bin\cudnn64_7.dll to C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin.
        Copy <installpath>\cuda\ include\cudnn.h to C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\include.
        Copy <installpath>\cuda\lib\x64\cudnn.lib to C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\lib\x64.
    Set the following environment variables to point to where cuDNN is located. To access the value of the $(CUDA_PATH) environment variable, perform the following steps:
        Open a command prompt from the Start menu.
        Type Run and hit Enter.
        Issue the control sysdm.cpl command.
        Select the Advanced tab at the top of the window.
        Click Environment Variables at the bottom of the window.
        Ensure the following values are set:

        Variable Name: CUDA_PATH 
        Variable Value: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0
"""

**FIFTH** 
Follow the Tensorflow download instructions [from here](https://www.tensorflow.org/install/pip)
	(I did a pip install to the system following the instructions there for tensorflow-gpu)
	
"""
 Choose one of the following TensorFlow packages to install from PyPI:

    tensorflow —Current release for CPU-only (recommended for beginners)
    tensorflow-gpu —Current release with GPU support (Ubuntu and Windows)
    tf-nightly —Nightly build for CPU-only (unstable)
    tf-nightly-gpu —Nightly build with GPU support (unstable, Ubuntu and Windows)

Package dependencies are automatically installed. These are listed in the setup.py file under REQUIRED_PACKAGES. 

	Install
		```python
		pip3 install --user --upgrade tensorflow  # install in $HOME```
	Verify Install from command prompt
		```python
		python3 -c "import tensorflow as tf; tf.enable_eager_execution(); print(tf.reduce_sum(tf.random_normal([1000, 1000])))"```
"""

**SIXTH** 
After install I went to CommandPrompt and started a Python session (python 3.6)
	in the Python session I ran 
	
	```import tensorflow as tf
	sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))```
	
	and it returned 
	
"""

	2018-12-26 10:17:00.071546: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2
	2018-12-26 10:17:00.470180: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1432] Found device 0 with properties:
	name: GeForce GTX 1070 Ti major: 6 minor: 1 memoryClockRate(GHz): 1.683
	pciBusID: 0000:08:00.0
	totalMemory: 8.00GiB freeMemory: 6.61GiB
	2018-12-26 10:17:00.476602: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1511] Adding visible gpu devices: 0
	2018-12-26 10:21:07.978605: I tensorflow/core/common_runtime/gpu/gpu_device.cc:982] Device interconnect StreamExecutor with strength 1 edge matrix:
	2018-12-26 10:21:07.980844: I tensorflow/core/common_runtime/gpu/gpu_device.cc:988]      0
	2018-12-26 10:21:07.982108: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1001] 0:   N
	2018-12-26 10:21:07.983572: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 6368 MB memory) -> physical GPU (device: 0, name: GeForce GTX 1070 Ti, pci bus id: 0000:08:00.0, compute capability: 6.1)
	Device mapping:
	/job:localhost/replica:0/task:0/device:GPU:0 -> device: 0, name: GeForce GTX 1070 Ti, pci bus id: 0000:08:00.0, compute capability: 6.1
	2018-12-26 10:21:07.990866: I tensorflow/core/common_runtime/direct_session.cc:307] Device mapping:
	/job:localhost/replica:0/task:0/device:GPU:0 -> device: 0, name: GeForce GTX 1070 Ti, pci bus id: 0000:08:00.0, compute capability: 6.1	
"""
