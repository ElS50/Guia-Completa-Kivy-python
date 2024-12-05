## Guía Completa: Crear una App con KivyMD

### ¿Qué es KivyMD?

#### KivyMD es una extensión de Kivy que implementa el diseño Material Design de Google. Ofrece widgets predefinidos como botones flotantes, barras de navegación, menús, tarjetas, y mucho más.

### Ventajas de usar KivyMD:

#### Apariencia profesional y moderna.
#### Componentes diseñados para aplicaciones móviles.
#### Fácil integración con Kivy

### Instala KivyMD
#### Instala KivyMD directamente desde PyPI:

        pip install kivymd

#### Si ya tienes Kivy instalado, actualízalo para evitar problemas:

        pip install --upgrade kivy

### Estructura de Proyecto
#### Crea una estructura ordenada para tu proyecto:

        MiAppKivyMD/
        │
        ├── main.py             # Archivo principal
        ├── app.kv              # Archivo de diseño (opcional)
        ├── assets/             # Carpeta para imágenes, íconos, etc.
        ├── env/                # Entorno virtual (opcional)
        └── buildozer.spec      # Archivo de configuración (para Android, opcional)


## Tu Primera App con KivyMD
####  Crear la estructura básica
#### En el archivo main.py, escribe lo siguiente:

        from kivymd.app import MDApp
        from kivymd.uix.label import MDLabel
        from kivymd.uix.button import MDRaisedButton
        from kivy.uix.boxlayout import BoxLayout

        class MainLayout(BoxLayout):
            def __init__(self, **kwargs):
                super().__init__(**kwargs)
                self.orientation = "vertical"
                
                # Agregar un Label de Material Design
                label = MDLabel(
                    text="¡Hola, KivyMD!",
                    halign="center",
                    theme_text_color="Primary",
                    font_style="H4"
                )
                self.add_widget(label)

                # Agregar un botón de Material Design
                button = MDRaisedButton(
                    text="Presióname",
                    pos_hint={"center_x": 0.5},
                    on_release=self.on_button_press
                )
                self.add_widget(button)

            def on_button_press(self, instance):
                print("¡Botón presionado!")

        class MiAppKivyMD(MDApp):
            def build(self):
                # Establece un tema global para tu app
                self.theme_cls.primary_palette = "Blue"
                self.theme_cls.theme_style = "Light"  # Cambia a "Dark" para modo oscuro
                return MainLayout()

        if __name__ == "__main__":
            MiAppKivyMD().run()


## Introducción al KV Language con KivyMD
#### KivyMD también soporta el lenguaje KV para separar la lógica de la interfaz gráfica.

        Archivo KV: app.kv
## 

        BoxLayout:
            orientation: "vertical"

            MDLabel:
                text: "¡Hola, KivyMD!"
                halign: "center"
                theme_text_color: "Primary"
                font_style: "H4"

            MDRaisedButton:
                text: "Presióname"
                pos_hint: {"center_x": 0.5}
                on_release: app.on_button_press()


## Archivo Python: main.py
#### Modifica main.py para trabajar con el archivo KV:

        from kivymd.app import MDApp

        class MiAppKivyMD(MDApp):
            def build(self):
                self.theme_cls.primary_palette = "Blue"
                self.theme_cls.theme_style = "Light"
                return

            def on_button_press(self):
                print("¡Botón presionado!")

        if __name__ == "__main__":
            MiAppKivyMD().run()

## Widgets Populares en KivyMD
####  Barra de Navegación Inferior (Bottom Navigation)

        from kivymd.uix.bottomnavigation import MDBottomNavigation, MDBottomNavigationItem

        class MainLayout(MDBottomNavigation):
            def __init__(self, **kwargs):
                super().__init__(**kwargs)
                self.add_widget(MDBottomNavigationItem(
                    name='screen 1',
                    text='Home',
                    icon='home',
                    on_tab_press=self.show_home_screen
                ))
                self.add_widget(MDBottomNavigationItem(
                    name='screen 2',
                    text='Settings',
                    icon='cog',
                    on_tab_press=self.show_settings_screen
                ))

            def show_home_screen(self, *args):
                print("Pantalla Home activada")
            
            def show_settings_screen(self, *args):
                print("Pantalla Configuración activada")

### Botón Flotante (FAB)


        from kivymd.uix.button import MDFloatingActionButton

        button = MDFloatingActionButton(
            icon="plus",
            pos_hint={"center_x": 0.5, "center_y": 0.5},
            on_release=lambda x: print("FAB presionado")
        )

### Tarjetas (Cards)

        from kivymd.uix.card import MDCard

        card = MDCard(
            orientation="vertical",
            size_hint=(None, None),
            size=("280dp", "180dp"),
            pos_hint={"center_x": 0.5, "center_y": 0.5},
            ripple_behavior=True
        )

### Diálogos

        from kivymd.uix.dialog import MDDialog

        dialog = MDDialog(
            title="Hola",
            text="Este es un diálogo en KivyMD",
            buttons=[
                MDRaisedButton(text="Aceptar", on_release=lambda x: dialog.dismiss())
            ]
        )
        dialog.open()

## Personalización del Tema
#### Cambiar la paleta de colores

        self.theme_cls.primary_palette = "Green"  # Cambia a otro color como "Red", "Purple"

#### Habilitar modo oscuro

        self.theme_cls.theme_style = "Dark"

## Empaquetar para Android con Buildozer

####  Instala Buildozer

        pip install buildozer

## Configura Buildozer
#### Genera un archivo buildozer.spec:

        buildozer init

### Configura lo siguiente en el archivo:

#### title: Título de tu app.
#### source.include_exts: Archivos .kv, imágenes, etc.
#### requirements: Incluye kivymd.


###  Genera el APK

        buildozer -v android debug

































