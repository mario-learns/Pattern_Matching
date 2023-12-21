# Perf-Finder Application

 "Perfs" are what we use to measure the performance of individual cameras using GStreamer.
 
 We, the analysts, would get multiple lines of output that looked liked the following : GPU [1] PERF: [18663@0] 2.00  |  [18665@1] 2.00  |  [18667@2] 2.00  |  [18669@3] 2.00  | 

A positive match would be indicated by @- : [18663@-] 0.00

With no automation, the cyber analysts were becoming fatigued losing patience and motivation when there are 100's of line of entries to look at for the @- patterns to indicate a down camera.

# Imported packages
import re

import argparse

import sys

import tkinter as tk

from tkinter import scrolledtext

import subprocess

# Package required in order to bring up the GUI.
required_packages = ["tkinter"]

def check_install_package(package_name):
    try:
        __import__(package_name)
        return True
    except ImportError:
        return False

def install_package(package_name):
    subprocess.check_call([sys.executable, "-m", "pip", "install", package_name])

# Will look for a the pattern '@-' and format the camera ID surrounded by brackets
def process_log(log_content):
    log_content_no_whitespace = re.sub(r'\s', '', log_content)
    
    pattern = r'\[(\d+)@-?\]'
    numbers_in_brackets = re.findall(pattern, log_content_no_whitespace)
    sorted_unique_numbers = sorted(set(numbers_in_brackets), key=int)
    formatted_numbers = " ".join([f"[{number}]" for number in sorted_unique_numbers])
    output_string = f"Number of matches: {len(sorted_unique_numbers)}\n{formatted_numbers}"
    
    return output_string
# Installing tkinter - Look for more efficient way to write this.
def main():
    for package in required_packages:
        if not check_install_package(package):
            print(f"Installing {package}...")
            install_package(package)

    parser = argparse.ArgumentParser(description="Parses analyst perf input and prints 0-perfs.")
    args = parser.parse_args()
    
    print("Paste the perfs into the file by right clicking. Press Ctrl+Z followed by Enter when you're done.")
    log_content = sys.stdin.read()
    
    output_string = process_log(log_content)
    
    root = tk.Tk()
    root.title("Filtered Output")
    
    text_widget = scrolledtext.ScrolledText(root, wrap=tk.WORD, width=50, height=20)
    text_widget.insert(tk.END, output_string)
    text_widget.pack(padx=10, pady=10)
    text_widget.configure(state="disabled")
    
    root.mainloop()

if __name__ == "__main__":
    main()


# Simple GUI of application asking for the "perfs".
![image](https://github.com/mario-learns/Pattern_Matching/assets/72238378/b84a6710-1dc6-4d18-ad5b-eec715857134)


# An example of how many lines of logs analysts are responsible for looking at. This is just one client's server. A single client could have more than one server at thier site.
![image](https://github.com/mario-learns/Pattern_Matching/assets/72238378/de76a99e-51c2-4c7f-bd58-5619b1ac2c74)


# We copy and paste the log information from the containerized software into the application.
![image](https://github.com/mario-learns/Pattern_Matching/assets/72238378/48f657d2-a785-45be-85a6-8986b408bc01)


# Press CTRL + Z to commit and begin the pattern matching. You will get the following pop-up using tkinter.
![image](https://github.com/mario-learns/Pattern_Matching/assets/72238378/7e4769b0-0d5c-4653-97c7-a150c901c7bf)

