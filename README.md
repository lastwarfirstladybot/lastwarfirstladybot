# Last War First Lady Bot Automation

This repository provides tools designed for use with BlueStacks to automate the First Lady role in the mobile game Last War. The macro will open each role and auto-approve applicant lists after scrolling down.

## Contents

This repository contains the following files:

1. **First Lady Automation With Conquerors Buff.json**  
2. **First Lady Automation Without Conquerors Buff.json**  
   - These files are BlueStacks macros that can be imported directly using the BlueStacks Macro Manager.
3. **FirstLadyAutomation.py**  
   - A Python script that performs the same functions as the macros with the added benefit of dismissing player roles after a set threshold.

---

## BlueStacks Macro Setup

### Importing and Running Macros
1. Open **BlueStacks**.
2. Navigate to **Macro Manager**.
3. Click **Import** and select either `First Lady Automation With Conquerors Buff.json` or `First Lady Automation Without Conquerors Buff.json`.
5. Start on the role selection screen and **run** the applicable macro. If using Conquerors buff, scroll down before running.

---
## Python Script Setup

The Python script provides the same functionality of the BlueStacks macros with the added benifit of dismissing players after they have been in a role for 6+ minutes. However, setting up the script requires configuring **screen coordinates** to match your specific system. Below are methods to streamline the process of finding these coordinates.
<br>*Note*: This script is not dependent on BlueStacks software.

---

### Finding Screen Coordinates  

Two Python snippets are provided to help you identify and configure the required coordinates:

---

#### 1. **Get Cursor Position**
This script prints the current cursor position every 3 seconds. Use it to find the coordinates of specific screen elements:  

```python
import pyautogui
import time

while True:
    time.sleep(3)  # Adjust delay as needed
    x, y = pyautogui.position()
    print(f"({x}, {y})")
```


#### 2. **Find coordinate region:**
This script allows you to visually select a region on the screen using a screenshot. It will output the selected rectangle's coordinates and dimensions:  

```python
import pyautogui
from PIL import Image
import matplotlib.pyplot as plt
import matplotlib.patches as patches

screenshot = pyautogui.screenshot()
screenshot_np = pyautogui.screenshot(region=None).convert('RGB')
def onselect(eclick, erelease):
    global rect
    rect = patches.Rectangle(
        (eclick.xdata, eclick.ydata),
        erelease.xdata - eclick.xdata,
        erelease.ydata - eclick.ydata,
        linewidth=1, edgecolor='r', facecolor='none'
    )
    ax.add_patch(rect)
    plt.draw()
fig, ax = plt.subplots(1)
ax.imshow(screenshot_np)
rect = None
toggle_selector = plt.gcf().canvas.mpl_connect('button_press_event', onselect)
plt.show()
