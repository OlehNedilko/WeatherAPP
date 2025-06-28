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
### Result:
Наш проєкт WeatherApp, був створений на мові програмування [Python](https://www.python.org/). Його функція: показувати погоду у режимі реального часу. Ви можете передивитися [модулі](#modules) які ми використали при створенні цього додатку. Додаток WeatherApp дуже зручний та корисний у повсякденному житті, у додатку зроблений дуже простий дизайн що робить використання додатку дуже простим. Додаток показує дуже точну інформацію, тому-що ми використали найточніші Api та модулі. Також ви можете передивитися [зміст](#зміст) проєкту та ознайомитися з ним.
