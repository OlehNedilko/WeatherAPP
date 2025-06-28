# WEATHER APPLICATION

![](static/icon/big%20screen.png)

Цей проект розроблено з метою ознайомлення із роботою API, принципом отримання даних від віддаленого серверу, вмінням їх обробляти, структурувати та застосовувати у своємо проєкті. А саме застосовувалось API такого веб-ресурсу як [OpenWeatherMap](https://openweathermap.org). Проєкт допоможе розібратися із роботою файлів JSON, як правильно отримувати та зберігати дані у файлах з типом .json. Та познайомити користувача з інтерфейсом застосунку розробленим за допомогою пакету [CustomTkinter](https://customtkinter.tomschimansky.com)

### Зміст:
- [Основні модулі проєкту](#modules)
- [Розгортання проєкту](#download)
- [Створення віртуального оточення проєкту](#venv)
- [Завантаження модулей до віртуального оточення](#download-venv)
- [Старт проєкту](#start-project)
- [Основні механіки проєкту](#mechanics)
- [Висновок по проєкту](#result)

### Modules:
Всі модулі
1. [customtkinter](https://customtkinter.tomschimansky.com)
2. [json](https://docs.python.org/3/library/json.html)
3. [colorama](https://pypi.org/project/colorama/)
4. [os](https://docs.python.org/uk/3.13/library/os.html)
5. [requests](https://pypi.org/project/requests/)
6. [pillow](https://pypi.org/project/pillow/)
7. [datetime](https://docs.python.org/3/library/datetime.html)


### Download:
Завантаження проєкту
- ##### Git clone:

    - Отримати посилання для клонування проєкту

    ![](static/icon/clone_link.png)

    - Відкрити VSCode --> у Explorer VSCode відкрити папку для збереження склонованого проєкту --> та у Terminal прописати команду: 
    - `git clone https://github.com/WorldIT-academy/WeatherApp.git`

    ![](static/icon/clone_command.png)

    - Відкрити каталог, який ви склонували у Explorer VSCode
    
### Venv:

#### Windows:
```python
python -m venv venv

source venv/Scripts/activate
```

#### MacOS:
```python
python3 -m venv venv

source venv/bin/activate
```

### Download requirements:

#### Windows
```python
pip install -r requirements
```

#### MacOS
```python
pip3 install -r requirements
```

### Start project:
Cтарт проєкту:
![Снимок](https://github.com/user-attachments/assets/839bdee0-634b-4d06-bdfe-587acc9771ab)

### Mechanics:
Основні механіки проєкту:
```python
import customtkinter as ctk
from ..mainframe import screen

class Horizontal_Scroll(ctk.CTkScrollableFrame):
    def __init__(self, child_master, width, height, border_w, border_color, corner_radius, x, y):
        ctk.CTkScrollableFrame.__init__(
            self,
            master = child_master,
            width = width,
            height = height,
            border_width = border_w,
            border_color = border_color,
            corner_radius = corner_radius,
            fg_color = "#3c5e85",
            orientation = "horizontal"
        )
        self.place(x = x, y = y)
        self.grid_rowconfigure(0, weight=1)

h_s = Horizontal_Scroll(screen, 818, 240, 3, "white", 20, 369, 500) 
```
```python
import customtkinter as ctk
from ..mainframe import screen

class Info_Container(ctk.CTkFrame):
    def __init__(self, child_master, width, height, x, y):
        ctk.CTkFrame.__init__(
            self,
            master = child_master,
            width = width,
            height = height,
            fg_color = "#91bdc7"   
        )
        self.place(x = x, y = y)

        self.grid_propagate(False)

        self.grid_rowconfigure(0, weight=1)
          
        self.grid_columnconfigure(0, weight=1)
        self.grid_columnconfigure(1, weight=1)
        self.grid_columnconfigure(2, weight=1)

info_cont = Info_Container(screen, 865, 455, 369, 25)
```

```python
import customtkinter as ctk
from .scroll_frame import vertical_scroll
import requests
import json
import os
import datetime
import zoneinfo
from timezonefinder import TimezoneFinder


class City_Frame(ctk.CTkFrame):
    def __init__(self, child_master, city_name, time, temp, condition, min_max):
        ctk.CTkFrame.__init__(
            self,
            master = child_master,
            width = 236,
            height = 100,
            border_width = 2,
            border_color = "#FFFFFF",
            fg_color = "#91bdc7"
        )
        self.pack(anchor = "center", pady = 7)
        
        self.grid_propagate(False)
        self.grid_columnconfigure(0, weight=1)
        self.grid_columnconfigure(1, weight=1)

        self.grid_rowconfigure(0, weight=1)
        self.grid_rowconfigure(1, weight=1)
        self.grid_rowconfigure(2, weight=1)

        self.city_label = ctk.CTkLabel(
            master = self,
            text = city_name,
            font = ("Comic Sans MS", 25)
        )
        self.city_label.grid(row = 0, column = 0, sticky = "w", padx=(10,0), pady=(10,0))

        self.time_label = ctk.CTkLabel(
            master = self,
            text = time,
            font = ("Arial", 14)
        )
        self.time_label.grid(row = 1, column = 0, sticky = "w", padx=(10,0), pady=(0,10))

        self.temp_label = ctk.CTkLabel(
            master = self,
            text = temp,
            font = ("Arial", 35)
        )
        self.temp_label.grid(row = 0, column = 1, sticky = "e", padx=(0,10), pady=(10,0))

        self.condition_label = ctk.CTkLabel(
            master = self,
            text = condition,
            font = ("Arial", 16)
        )
        self.condition_label.grid(row = 2, column = 0, sticky = "w", padx=(10,0), pady=(10,10))

        self.min_max_label = ctk.CTkLabel(
            master = self,
            text = min_max,
            font = ("Arial", 14)
        )
        self.min_max_label.grid(row = 2, column = 1, sticky = "e", padx=(0,10), pady=(10,10))

cities = ["Kyiv", "Budapest", "Warsaw", "Vienna", "Prague", "Berlin", "Milan", "Paris", "London", "NewYork"] 

my_city_info = requests.get("https://ipinfo.io/json")
my_city_name = my_city_info.json()["city"]

if my_city_name in cities:
    cities.remove(my_city_name)

cities.insert(0, my_city_name)
    
db_data = {}

for city in cities:

    url = f"http://wttr.in/{city}?format=j1"
    result = requests.get(url).json()
    
    temp = result["current_condition"][0]["temp_C"] + "°"
    condition = result["current_condition"][0]["weatherDesc"][0]["value"]
    if len(condition) > 15:
        condition = condition[0:15] + "..."
    min_max = f"min:{result['weather'][0]['mintempC']} max:{result['weather'][0]['maxtempC']}"
    
    my_lat = result["nearest_area"][0]["latitude"]
    my_long = result["nearest_area"][0]["longitude"]
    
    timezona_name = TimezoneFinder().timezone_at(lat = float(my_lat), lng = float(my_long))
    zona = zoneinfo.ZoneInfo(timezona_name)
    my_time = datetime.datetime.now(zona)
    time = my_time.strftime("%H:%M")
    
    db_data[f"{city}"] = {
        "day_week": my_time.strftime("%A"),
        "date": my_time.strftime("%d.%m.%Y"),
        "time": time,
        "api_data": result
    }

    cf = City_Frame(vertical_scroll, city, time, temp, condition, min_max)

my_path = os.path.abspath(__file__)
my_dir = os.path.dirname(my_path)
my_db = my_dir + "\\..\\..\\data_base.json"

with open(my_db, "w") as file:
    json.dump(db_data, file, indent=4)
```

### Result:
Наш проєкт WeatherApp, був створений на мові програмування [Python](https://www.python.org/). Його функція: показувати погоду у режимі реального часу. Ви можете передивитися [модулі](#modules) які ми використали при створенні цього додатку. Додаток WeatherApp дуже зручний та корисний у повсякденному житті, у додатку зроблений дуже простий дизайн що робить використання додатку дуже простим. Додаток показує дуже точну інформацію, тому-що ми використали найточніші Api та модулі. Також ви можете передивитися [зміст](#зміст) проєкту та ознайомитися з ним.
