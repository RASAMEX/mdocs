# mdocs

mdocs allows you to extract docstrings from Python functions to create a documentation file in Markdown format. It is designed as an alternative for projects that consist of just a few functions and do not require more sophisticated tools. We will obtain an MD file that can easily be linked to the README of our repository to present accessible and well-organized technical documentation to clients or users.

## Module mdocs.py
### main( )

Main function to parse command-line arguments and execute the necessary actions.

This function performs the following steps:
1. Reads the configuration file ('config.ini') to obtain the version and author information.
2. Displays a banner with the version number.
3. Initializes an argument parser with the following options:
    - A positional argument 'source' for specifying the path of the source file to analyze.
    - A '-c/--config' flag to access the initial configuration menu.
    - A '-v/--verbose' flag to enable verbose logging mode (debugging).
4. Based on the arguments provided, it either:
    - Runs the `starter` function if the configuration flag is set.
    - Executes the `execute` function with the provided source path if specified.
    - Displays a help message if no arguments are provided.

Args:
- None

Returns:
- None



## Module creation_functions.py
### read_config_file( )

Reads and parses a JSON configuration file.

This function attempts to open and read the specified configuration file, 
returning the parsed data if successful. It handles errors such as the file 
not being found or invalid JSON format.

Args:
- config_file (str): The path to the configuration file.

Returns:
- dict: The parsed configuration data from the file, or None if an error occurs.

Example:
```
    >>> read_config_file('mdocs_settings.json')
    INFO - 'The configuration file has been read successfully'
    DEBUG - {"title": "Test Project", "description": "This is a test project", "developer": "Your name", "mail": "Your email", "link": "Your link"}
```


### find_python_files( )

Recursively searches for Python files in the specified directory.

This function scans the provided directory for `.py` files and returns
a list of their paths.

Args:
- directory (str): The directory path to search for Python files.

Returns:
- list: A list of file paths to Python files in the directory, or None if the directory is invalid.



### extract_functions_with_docstring( )

Extracts functions and their docstrings from a list of Python files.

This function parses each Python file in the provided list, extracting the 
function names and their associated docstrings, if available.

Args:
- paths (list): A list of file paths to Python files.

Returns:
- list: A list of tuples containing the module name and a list of function names with their docstrings.



### format_section( )

Formats a specific section (e.g., Args, Returns) in a function's docstring.

This function searches for the specified section in the docstring and formats it 
as a list, if found.

Args:
- section_name (str): The name of the section to format (e.g., 'Args', 'Returns').


- docstring (str): The function's docstring to format.

Returns:
- str: The formatted docstring with the specified section formatted as a list.



### format_example( )

Formats the 'Example' section in a docstring.

This function looks for an 'Example:
```' section in the docstring and formats it
within code blocks for better readability.

Args:
- docstring (str): The function's docstring to format.

Returns:
- str: The formatted docstring with the 'Example' section in code blocks.

```


### write_to_md( )

Generates a Markdown documentation file from Python files and configuration data.

This function reads the configuration file, scans the source directory for Python 
files, extracts the functions and their docstrings, and writes the formatted 
documentation to the specified output file in Markdown format.

Args:
- source_file (str): The path to the source directory containing Python files.


- config_file (str): The path to the JSON configuration file.


- output_file (str): The path to the output Markdown file.

Returns:
- None



## Module config_functions.py
### validate_required_fields( )

Prompts the user for input and ensures that a value is provided.

This function repeatedly prompts the user for input until a non-empty
value is provided. It is used for required fields where user input is mandatory.

Args:
- message (str): The message to display to the user when asking for input.

Returns:
- str: The non-empty input provided by the user.



### starter_config( )

Creates an initial configuration file with user-provided project details.

This function:
1. Checks if a configuration file already exists at the specified location.
2. If a file exists, asks the user if they want to overwrite it.
3. Prompts the user for various required and optional project information such as project name, description, developer/company name, contact email, and repository link.
4. Writes the collected data to the specified configuration file in JSON format.

Args:
- filename (str): The name of the configuration file to create or overwrite.

Returns:
- None



