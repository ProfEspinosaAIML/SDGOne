# SDGOne
Synthetic Data Generation - Trial One
June 2024

This experiment is hosted in GitHug at:
https://github.com/ProfEspinosaAIML/SDGOne 


PART 1 - Set up the work environment
The environment setup assumes you are working on Visual Studio Code and a PowerShell (PS) terminal. 

Follow the instructions below:

1. Install Miniconda: https://docs.anaconda.com/free/miniconda/ 

2. Download and install, in this case, for Windows 11 (64-bit) using the quick command line install download:

curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe -o miniconda.exe

3. Run the installer:

 .\miniconda.exe

4. Follow the installation as explained in: https://realpython.com/python-windows-machine-learning-setup/ 

5. Remove the installer:  

del miniconda.exe

6. As Anaconda was not included in the PATH environment variable, its commands won’t work in the Windows default command prompt. To use the distribution, you should start its own command prompt, which can be done by clicking on the Start button and on Anaconda Prompt under Anaconda3 (64 bit)

7. When the prompt opens, you can check if Conda is available by running:

conda --version

8. To get more information about the installation, you can run:

conda info

9. Add miniconda to the Windows PATH environment variable. The paths you need to add are:
C:\Users\you\AppData\Local\miniconda3\
C:\Users\you\AppData\Local\miniconda3\Scripts\
C:\Users\you\AppData\Local\miniconda3\Library\bin

10. Reload the developer environment

.\conda.exe
or
./conda

11. Confirm that you can see the base miniconda environment

PS C:\Users\you\AppData\Local\miniconda3\Scripts> ./conda env list
# conda environments:
#
base                     C:\Users\Eespinosa\AppData\Local\miniconda3


PART 2 - Set up Jupyter Notebooks to develop the Generative Adversarial Network (GAN) following the tutorial in:
https://realpython.com/generative-adversarial-networks/ 

1. To begin, create a conda environment and activate it:

$ ./conda create --name SDGOne python=3.8

2. Confirm that the environment was correctly set up:

Preparing transaction: done
Verifying transaction: done
Executing transaction: done

3. Activate the environment:
$ ./conda init

4. Reload the developer environment

5. Activate the environment:
$ ./conda activate SDGOne

6. Install the necessary packages inside the environment:

$ conda install -c pytorch pytorch=1.4.0
$ conda install matplotlib jupyter

7. We will use Jupyter Notebooks to run the code, so register the conda SDGOne environment allowing us to create Notebooks using it as the kernel:

$ python -m ipykernel install --user --name SDGOne



PART 3 - Develop the Generative Adversarial Network (GAN) following the tutorial in:
https://realpython.com/generative-adversarial-networks/ 

1. Open Jupyter Notebook by running jupyter notebook on VSCode. 

2. Create a new Notebook by clicking New.

3. CLick "Select Kernel" and then SDGOne.

4. The Notebook has one code snippet:
import torch

ERROR Log:
import torch

Causes an error:
ImportError: DLL load failed while importing _C: The specified module could not be found
To confirm the root cause, I ran:
$ conda activate SDGOne
$ python -c "import torch; print(torch.__version__)"

That output:
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "C:\Users\Eespinosa\AppData\Local\miniconda3\envs\SDGOne\lib\site-packages\torch\__init__.py", line 81, in <module>
    from torch._C import *
ImportError: DLL load failed while importing _C: The specified module could not be found.

which seems to confirm that the problem is with the PyTorch Installation.

So countermeasure was to upgrade PyTorch and Pythonon on the SDGOne environment:

$ conda deactivate
$ conda env remove --name SDGOne
$ conda create --name SDGOne python=3.9
$ conda activate SDGOne
$ conda install pytorch torchvision torchaudio cpuonly -c pytorch
$ conda install matplotlib jupyter
$ python -m ipykernel install --user --name SDGOne --display-name "Python (SDGOne)"
$ python -c "import torch; print(torch.__version__)"




 