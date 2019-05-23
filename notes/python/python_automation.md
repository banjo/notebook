# Python

## Automation
- [PyAutoGui](#pyautogui)
  * [Match pixel](#match-pixel)
  * [Look for picture](#look-for-picture)
- [Keyboard](#keyboard)
  * [Use hotkey](#use-hotkey)
- [Excel](#excel)
  * [Read excel file.](#read-excel-file)
  * [Write to excel.](#write-to-excel)
- [Selenium](#selenium)
  * [Change tab](#change-tab)
  * [Find element by xpath](#find-element-by-xpath)
  * [Look for loaded page](#look-for-loaded-page)
- [Other](#other)
  * [Print in color](#print-in-color)

## PyAutoGui

### Match pixel
See if pixel matchens a specific color.

```python
if pyautogui.pixelMatchesColor(25, 162, (255, 255, 255)):
            input("Hittar ingen kund med nummer " + kundnummer)
            exit()
```

### Look for picture
See if a picture exists on a screen.

```python
import pyautogui

def letaBild (bild, region):
    position = pyautogui.locateCenterOnScreen(bild, region=region)
    if not position == None:
        return True
    else:
        return False
```

## Keyboard

### Use hotkey
```python
import keyboard, time

# ctrl + hotkey
keyboard.press("ctrl")
keyboard.press('a')
time.sleep(0.5)
keyboard.release('a')
keyboard.release("ctrl")

# backspace
keyboard.press_and_release("backspace")# backspace
time.sleep(1)
```

## Excel

### Read excel file.

```python
import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile

# read from excel in df
df = pd.read_excel('name_of_excel.xlsx', sheet_name='name_of_sheet')

# get a list with the name "total"
total = df['total']
```

### Write to excel.
```python
import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile

# save to file to the same directory as the file
dir_path = os.path.dirname(os.path.realpath(__file__))
dir_path = os.path.join(dir_path, "example.xlsx")

# create the file
df = pd.DataFrame(databas) # dictionary with lists (String, list)
df.to_excel(dir_path)
```

Alternative way:
```python
writer = ExcelWriter("example.xlsx")
df2 = pd.DataFrame({"title":python_list, "another_title":another_python_list})
df2.to_excel(writer, "Sheet1", index=False)
writer.save()
```

## Selenium

### Change tab
```python
browser = driver
```
Change to newly opened tab.
```python
browser.switch_to.window(browser.window_handles[-1])
```
Change to main window.
```p
browser.switch_to.window(browser.window_handles[0])
```

### Find element by xpath
```p
from selenium.common.exceptions import NoSuchElementException

def findxPath(xpath):
    try:
        rad = browser.find_element_by_xpath(xpath)
        print("Found element")
        return rad.location
    except NoSuchElementException:
        print("Did not find element")
```

### Look for loaded page
Looks for a loaded page - as well as if it is a correct page. Looks for it based on the xpath. 
Returns true if it finds it.

```p
from selenium.webdriver.support import expected_conditions as EC
from selenium.common.exceptions import TimeoutException

def loadPage(xpath, browser):
    try:
        timeout = 5
        element_present = EC.presence_of_element_located((By.XPATH, xpath))
        WebDriverWait(browser, timeout).until(element_present)
        return True
    except TimeoutException:
        print("Hittade inte sidan.")
        return False
```

## Other

### Automation class
Class with the most basic automations

```p
import keyboard
import pyautogui
import time
import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile


class Auto:

    start = None
    end = None

    def click(self, x, y):
        """clicks on specified position
        
        Arguments:
            x {integer} -- x position
            y {integer} -- y position
        """
        pyautogui.click(x, y)
        time.sleep(1.5)

    def clear_text(self):
        """clears a field if it is marked
        """
        keyboard.press("ctrl")
        time.sleep(0.2)
        keyboard.press_and_release('a')
        time.sleep(0.2)
        keyboard.release("ctrl")
        keyboard.press_and_release("backspace")
        time.sleep(0.4)

    def find_picture(self, bild):
        """returns position if there is a picture, else it returs false
        
        Arguments:
            bild {.png file} -- a picture in .png
        
        Returns:
            boolean or position -- position if the picture exists, else false
        """
        position = pyautogui.locateCenterOnScreen(bild)

        if not position == None:
            x, y = position[0], position[1]
            return x, y
        else:
            return False

    def find_picture_in_region(self, bild, region):
        """returns position if there is a picture, else it returs false
        
        Arguments:
            bild {.png file} -- a picture in .png
        
        Returns:
            boolean or position -- position if the picture exists, else false
        """
        position = pyautogui.locateCenterOnScreen(bild, region=region)

        if not position == None:
            x, y = position[0], position[1]
            return x, y
        else:
            return False

    def get_excel(self, excel_name, sheet_name):
        """creates an pandas document from an excel file that can be read.
        
        Arguments:
            excel_name {excel file} -- the name of the excel file
            sheet_name {excel sheet} -- the name of the
        
        Returns:
            [pandas file] -- [returns the pandas file that can be used later]
        """
        return pd.read_excel(excel_name, sheet_name)

    def read_excel_column(self, excel_file, column_name):
        """returns a list of that column in the excel file
        
        Arguments:
            excel_file {pandas file} -- the pandas file that was created
            column_name {[string]} -- [the name of the column]
        
        Returns:
            [list] -- [list of everything in that column]
        """
        return excel_file[column_name]

    def start_time(self):
        self.start = time.clock()
    
    def end_time(self):
        self.end = time.clock()
    
    def work_time(self):
        """Returns time it took for a loop in seconds
        
        Returns:
            [integer] -- [seconds it took for a loop]
        """
        return round(self.end - self.start, 2)
    
    def append_to_file(self, name_of_file, text_string):
        """write to text file
        
        Arguments:
            name_of_file {.txt file} -- the name of the text file
            text_string {string} -- what you want to write to the text file
        """
        with open(name_of_file, "a") as text_file:
            print(text_string, file=text_file)

```
### Time
How to show how long time a loop takes

import time
`import time`

Begin the time before a loop:
`start = time.clock()`

End the time at the end of a loop:
`end = time.clock()`

Get the final time in seconds, with 2 decimals:
`final_time = round(end - time, 2)`

### Print in color

```p
from termcolor import colored
from colorama import init

# needs to be initialized to work on windows
init()

# example with green text
print(colored("this is green text", 'green'))
```

