# Miniconda
Is an alternative to [[Anaconda]] with onle 70mb download plus the [[Conda]] feature. 
Here is how to [download](https://docs.conda.io/en/latest/miniconda.html) it. 

To create an environment just follow this steps. Open the Miniconda promps
![[Pasted image 20220726091147.png]]

Go to your folder and create a new directory using `mkdir` [[File Manipulation Command]]
```shell
$ mkdir project
```

Move to this project and create an environment with the dependencies we need. The command is
```shell
$ conda create --prefix ./env matplotlib scikit-learn numpy pandas
```

Activate the environment by command `activate` along with the path of the created environment
```shell
$ conda activate "D:\StudyMaterial\Codes\MLProjects\sample_project_1\env"
```

You should see something like this replacing your base
![[Pasted image 20220726091759.png]]

Next is to open the [[Jupyter]] notebook
```shell
$ jupyter notebook
```

If it does not work, we need to install it
```shell
$ conda install jupyter
```

That's it.

