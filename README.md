# Image Metadata Hash Spoofing Tool

This standalone tool, packaged with `PyInstaller`, allows you to modify the metadata of an image file and generate a hash that matches a specified target hash prefix. The tool works by iterating over the metadata, adding incremental changes, and checking the resulting hash until a match is found.

## 📋 Prerequisites

 tools used;

- **Python** (for packaging the script using `PyInstaller`)
- **PyInstaller** (for creating the standalone executable)
- **Pillow** (Python library for image manipulation)
- **hashlib** (Python library for hashing functionality)

To install the necessary dependencies, you can run the following commands:

```bash
pip install Pillow pyinstaller


 # Tool Overview
 
The tool works by running the spoof.py script, which performs the following actions:

 ## calculate_hash(file_path, hash_algorithm="sha512"):

Calculates the hash of a file using the specified hash algorithm (default is sha512).
Reads the file in chunks and returns the hexadecimal hash of the file.
add_metadata(image_path, output_path, metadata):

Adds metadata to an image file, saving it in PNG format (converts to PNG if necessary).
Uses the PngInfo object from the Pillow library to embed metadata into the image.
modify_image_to_match_hash(target_prefix, original_path, altered_path, hash_algorithm="sha512"):

Modifies the metadata of an image iteratively until the hash matches the specified target hash prefix.
Adds incremental metadata changes and checks the hash after each modification.


 ## Usage
After packaging the script with PyInstaller, you can run the tool as a standalone executable. The usage is as follows:

.\spoof.exe <hexstring> <original_image> <altered_image>
Arguments:
<hexstring>: The target hash prefix you want to match. It should be a hexadecimal string, and the tool will attempt to find a hash that starts with this prefix.
<original_image>: The path to the original image file you want to modify.
<altered_image>: The path where the modified image will be saved.

- ** example**
'''.\spoof.exe 0x24 profile.jpg altered.jpg

- In this example, the tool will modify the image profile.jpg by adding metadata, iterating over the changes until it generates an image whose hash starts with 0x24. The resulting image will be saved as ared.jpg.
  
# Add to environment variable

Update the PATH:

Press Win + R, type sysdm.cpl, and press Enter.
Go to the Advanced tab and click Environment Variables.
Under System Variables, find and select the variable named Path, then click Edit.
Click New and add the path to the directory containing spoof.exe 

open powershell and run

'''spoof 0x24 original.jpg altered.jpg

## Notes
- The tool is packaged as a standalone executable, so you do not need Python or additional dependencies installed on the target machine.
- The tool is designed to work with PNG images. If the input image is not in PNG format, it will be automatically converted.
- The tool will continue to modify the image's metadata until it matches the specified hash prefix.
- The default hash algorithm is sha512, but you can change it by modifying the script.

##Spoof.py
Script Overview
- The script has the following core functions:

calculate_hash(file_path, hash_algorithm="sha512"):

- This function calculates the hash of a file using the specified hash algorithm (default is sha512).
- It reads the file in chunks and returns the hexadecimal hash of the file.
- add_metadata(image_path, output_path, metadata):

# This function adds metadata to an image file.
- It opens the image, adds the provided metadata, and saves the image in PNG format (converting to PNG if necessary).
-  metadata is added to the image using the PngInfo object from the Pillow library.
- modify_image_to_match_hash(target_prefix, original_path, altered_path, hash_algorithm="sha512"):

- This function iterates over the metadata and adds incremental changes until the hash of the altered image matches the specified target_prefix.
- It calls add_metadata to alter the image and checks if the hash of the modified image matches the desired hash prefix.
- The script will continue this process, incrementing the metadata and attempting to match the hash until a match is found.
Usage
To run the script, use the following command format:

python spoof.py <hexstring> <original_image> <altered_image>
