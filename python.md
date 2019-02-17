# Python

## Automation

### PyAutoGui

#### Match pixel
See if pixel matchens a specific color.

```python
if pyautogui.pixelMatchesColor(25, 162, (255, 255, 255)):
            input("Hittar ingen kund med nummer " + kundnummer)
            exit()
```

#### Look for picture
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

### Keyboard

#### Use hotkey
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

### Excel

#### Read excel file.

```python
import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile

# read from excel in df
df = pd.read_excel('name_of_excel.xlsx', sheet_name='name_of_sheet')

# get a list with the name "total"
total = df['total']
```

#### Write to excel.
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

### Selenium

#### Change tab
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

#### Find element by xpath
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

#### Look for loaded page
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

### Other

#### Print in color

```p
from termcolor import colored
from colorama import init

# needs to be initialized to work on windows
init()

# example with green text
print(colored("this is green text", 'green'))
```

