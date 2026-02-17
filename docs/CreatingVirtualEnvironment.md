# How to create your Python Environment on RaspberryPi

1. Install Python system wide in order to be able to create a virtual environment, in your termninal:

`sudo apt install python3`

This command will install Python inside the Linux machine, in order to install the packages inside the venv Python needs a package manager called **pip**.

`sudo apt install python3-pip`

2. Creat a directory for your python venv and change your directory to it:

`mkdir python_venv && cd python venv`

3. Declaring your directory as your python venv, in this way your machine will now that in this folder will be executed python scripts but also that will be installed python dependecies (packages):

`python3 -m venv .venv`

4. Venv activation, this step is very important, with this command your system will know that you are now inside your virtual environment and you can install packages and run scrpit using the resources that are available in this environment:

`source .venv/bin/activate`

After running the command you can see that (.venv) appeared and now you are inside your venv.

<img width="523" height="23" alt="image" src="https://github.com/user-attachments/assets/074a966a-3750-4248-bead-fdc4e279af49" />

5. Install the dependecies that you will use in your project using the pip command:

`pip install your_package`

6. Run scripts using the command:

`./your_script.py`

7. That's it now you have a running virtual environment.
