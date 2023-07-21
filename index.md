# BlueStamp ChatGPT Infinite Text Adventure 
My project implements ChatGPT’s OpenAI to create an endless game that gives players scenarios based on previous choices they make. My biggest takeaway from this project is realizing how resourceful the internet is, as it played a big part in reaching the end goal.


```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Justin D | Dublin High School | Software Engineer | Incoming Junior


![Headstone Image](File_000 (3).jpeg)
![Headstone Image](File_000 (2).jpeg)

# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/_DQFTfsj8S4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Since my previous milestone, I have finished the exterior design and managed/organized the interior to secure the raspberry pi from getting damaged. The biggest challenge I’ve had here at BlueStamp Engineering was just trying to figure out what my raspberry pi needed to run my game smoothly. I was able to overcome this by asking the right questions to pinpoint problems and fix them with a proper solution. I’d say the biggest triumph of this experience is Demo Night where I got to show off my working project to the rest of my classmates and their parents. Some key things I learned along my journey was being able to use the command line/terminal, VS Code, working with a raspberry pi, and having a better understanding of ChatGPT and its resources. In the future, I would like to implement a GUI into my project to further my knowledge and improve on my design. Lastly, through BlueStamp I feel as if I learned a lot about myself. I joined this program unsure if I wanted to pursue a career in engineering, but after my experience here I’m definitely going to settle in the engineering field.



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/qKQ7GKipk_Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My second milestone was to get my game up and running on my LCD. This immediately brought me to a problem as my API key ran out of tokens, so my game couldn’t use ChatGPT to generate prompts and options. I fixed this by getting a new API with tokens from my instructor and replacing my old API key that was on the pi. I was able to run the game smoothly on the LCD and I had the idea of making the game portable as a modification. I tried using an old portable charger of mine, but the pi required more power than it could give. I decided I was going to need a new one to help everything run properly. For my next milestoneI will try to create a GUI(graphical user interface), manage the wires on the interior, and design the exterior to be more engaging.

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/dvZ1CRHuXYE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was to get my raspberry pi to run the code of the game from my terminal. I was able to do this by getting my raspberry pi up and running through a monitor. I then learned how to remotely access(ssh) my pi to copy a repository that held all the code for the game. I wasn’t very familiar with the command line, but with help from my instructor and online videos I started to get the hang of it. After I copied the code, I needed to install Python requirements for my project, which led me to my first problem. The version of Python installed on my raspberry pi was 2.7.16, but the code of the game needed a newer version. I fixed this problem by learning different commands in the command line to help download a newer version of python which was 3.9.11. My next milestone is to get my game running on my LCD.

# Code
Here is the code I used to run my game! Make sure you setup an API Key to be able to use and pull from ChatGPT's resources.

```python
import logging

import pyfiglet
from generator.title import generate_title
from generator.figlet import generate_figlet_font
from generator.story import generate_story
from generator.backstory import generate_backstory
from generator.prompt import generate_prompt

logging.basicConfig(
    filename='game.log',
    filemode='a',
    format='%(asctime)s,%(msecs)d %(name)s %(levelname)s %(message)s',
    datefmt='%H:%M:%S',
    level=logging.DEBUG
)

logging.info("Starting new game")

logger = logging.getLogger('game')

theme = input("Enter a theme: ")
logger.debug(theme)
title = generate_title(theme)
logger.debug(title)
story_points = generate_story(title)
logger.debug(story_points)

player = {
    "health": 100,
    "energy": 100,
    "score": 0,
    "progress": 0,
}

# Display the game title
figlet_font = generate_figlet_font(title["TITLE"], title["TITLE DESCRIPTION"])
try:
    banner = pyfiglet.figlet_format(title["TITLE"], font=figlet_font)
except pyfiglet.FontNotFound:
    banner = pyfiglet.figlet_format(title["TITLE"])
print()
print(banner)
print()
print()

# Display the game backstory
backstory = generate_backstory({"title": title, "location": story_points[0]["location"]})
print(backstory)
print()

# Start the game
prompt = generate_prompt(title, story_points, player)
while player["progress"] < len(story_points):
    logger.debug(prompt)
    print("=========================================")
    print()
    print(prompt["text"])
    print()
    print("Your options are:")
    for i, option in enumerate(prompt["options"]):
        print(f"{i + 1}. {option}")
    print()
    choice = int(input("Enter your choice: "))
    print()
    prev_prompt = {"text": prompt["text"], "options": prompt["options"], "selected": prompt["options"][choice - 1]}
    prompt = generate_prompt(title, story_points, player, prev_prompt)

```

# Bill of Materials
These are the parts I used to either set up or build my project.

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| CanaKit Raspberry Pi 4 Starter Kit | Used for building/setting up my Raspberry Pi | $139.99 | <a href="https://www.amazon.com/CanaKit-Raspberry-4GB-Starter-Kit/dp/B07V5JTMV9/ref=asc_df_B07V5JTMV9/?tag=hyprod-20&linkCode=df0&hvadid=380145854123&hvpos=&hvnetw=g&hvrand=4328410909910130065&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9032032&hvtargid=pla-1004184582672&psc=1&tag=&ref=&adgrpid=85982211068&hvpone=&hvptwo=&hvadid=380145854123&hvpos=&hvnetw=g&hvrand=4328410909910130065&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9032032&hvtargid=pla-1004184582672"> Link </a> |
| Hosyond 7 Inch IPS LCD Touch Screen Display Panel | Displays game and provides touch screen to choose from options | $45.88 | <a href="https://www.amazon.com/Hosyond-Display-1024%C3%97600-Capacitive-Raspberry/dp/B09XKC53NH/ref=sr_1_3?crid=1CZRN1MHNP6SJ&keywords=hoysond+7+inch+IPS+LCD+touch+screen+display+panel&qid=1689552210&sprefix=hoysond+7+inch+ips+lcd+touch+screen+display+panel%2Caps%2C134&sr=8-3"> Link </a> |
| Wireless Keyboard and Mouse | Used to setup/access Raspberry Pi | $23.99 | <a href="https://www.amazon.com/Wireless-Keyboard-Full-Size-Desktops-Computer/dp/B07XDWCLYF/ref=sr_1_3?crid=3FL658R6GSFA1&keywords=wisfox+usb+computer+keyboard&qid=1689552497&sprefix=wisfox+usb+computer+keyboar%2Caps%2C147&sr=8-3"> Link </a> |

# Tools

| X-ACTO Knife | Used to cut out hole for LCD and to create enclosure for the Raspberry Pi |
| Hot Glue Gun | Used to glue cardboard enclosure to secure Raspberry Pi so it won't get damaged |

# My Resources
These are some of the guides/resources I used along the way.
- [ChatGPT Text Adventure Repository](https://github.com/somacdivad/gpt-text-adventure/tree/improved-game-workflow)
- [Installing Newer Version of Python](https://www.youtube.com/watch?v=Cj7NhuLkvdQ)
- [LCD Setup/Making Pi Portable Idea](https://www.youtube.com/watch?v=iTUT3i9urwI&t=265s)
- [How to Run Python in terminal](https://www.youtube.com/watch?v=8mSpxFU5YFg)

