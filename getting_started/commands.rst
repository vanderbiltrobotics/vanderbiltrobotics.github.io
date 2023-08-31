*******************
Command Line Basics
*******************
A lot of work on the programming team involves the terminal so here is a quick reference for 
getting comfortable with working in the terminal. Note that linux and macOS are both Unix operating systems.

GREAT

.. tabs::

  .. group-tab:: Unix

    .. code-block:: bash
      
      cd <folder-name>                  # Change current directory to specified folder
      pwd                               # Print working directory
      ls                                # List files & folders in the working directory
      clear                             # Clear the terminal screen (shortcut: ctrl + l)
      rm <file-name>                    # Remove a file 
      rm -rf <folder-name>              # Delete a folder
      mv <source-name> <dest-name>      # Move/rename a file
      cp <source-name> <dest-name>      # Copy a file
      cp -R <source-name> <dest-name>   # Copy a folder
      top                               # Show CPU usage      

  .. group-tab:: Windows

    .. code-block:: bash
      
      cd <folder-name>                  # Change current directory to specified folder
      cd                                # Print working directory
      dir                               # List files & folders in the working directory
      cls                               # Clear the terminal screen (shortcut: ctrl + l)
      del <file-name>                   # Remove a file 
      deltree <folder-name>             # Delete a folder
      move <source-name> <dest-name>    # Move/rename a file
      copy <source-name> <dest-name>    # Copy a file
      xcopy <source-name> <dest-name>   # Copy a folder
      mem                               # Show CPU usage

.. note:: 
  In order to go into the parent folder use :code:`cd ..`

Other Useful Unix Commands
==========================

- :code:`which` shows where an executable is installed on the path (ex: :code:`which python`)
- :code:`shutdown` must be run on the Jetson to properly shut it down before removing power source.
- :code:`ctrl` + :code:`c` will stop anything executing in the terminal (this is how you stop a node)
- :code:`code .` will open the current directory in vscode if vscode was added to the path as :code:`code`
- Use the pipe operator :code:`|` to send output to another command:
    - Ex: In order to find a file in a huge directory: :code:`ls | grep <file-name>`
- :code:`chmod +x <file-name>` will give a file executable permissions (chmod stands for change mode)
- :code:`>` will redirect the output from a previous command (e.g. :code:`ls > list.txt` writes the directories to the file)
    - :code:`>>` will append the output to the end of an existing file while :code:`>` overwrites
    - Ex: :code:`echo "source /opt/ros/foxy >> .bashrc` will append the sourcing command to your bashrc
- `More on Redirecting Output, Input, & Errors <http://www.penguintutor.com/linux/command-basics-reference>`_
