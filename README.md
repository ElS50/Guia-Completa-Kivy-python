# Guia-Completa-Kivy-python

## Guía Completa: Crear una App en Python con Kivy

#### Kivy es un framework de Python para desarrollar aplicaciones gráficas y multiplataforma. Sus principales características son:

#### Es compatible con Android, iOS, Windows, macOS y Linux.
#### Soporta diseño adaptable, lo que lo hace ideal para dispositivos con diferentes tamaños de pantalla.
#### Está basado en OpenGL, por lo que es eficiente para gráficos y animaciones.

## Configuración del Entorno

#### Paso 1: Instalar Python
#### Descarga la última versión de Python compatible con Kivy desde python.org.
#### Asegúrate de marcar la casilla "Add Python to PATH" durante la instalación.
#### Paso 2: Crear un entorno virtual
#### Es buena práctica trabajar en un entorno virtual para evitar conflictos entre bibliotecas.

        python -m venv env

### Activa el entorno Windows
        .\env\Scripts\activate 

### Desactiva el entorno Windows
        Desactive

### Instalar Kivy
Con el entorno activado, instala Kivy:

        pip install kivy

        pip install kivy_examples


### Estructura Básica de un Proyecto Kivy
#### Tu proyecto debería seguir una estructura ordenada. Aquí tienes una recomendación:

    MiProyecto/
    │
    ├── main.py             # Archivo principal
    ├── app.kv              # Archivo de diseño (KV Language)
    ├── assets/             # Carpeta de imágenes, sonidos, etc.
    ├── modules/            # Módulos adicionales (lógica separada)
    └── env/                # Entorno virtual (opcional)


### Archivo principal (main.py)
#### Este es el archivo que ejecutará tu aplicación. Contiene la lógica principal.

### Archivo de diseño (app.kv)
#### Este archivo define la interfaz gráfica (UI) usando el lenguaje KV, que es limpio y fácil de leer.

### Tu Primera App con Kivy
#### Paso 1: Crear el archivo principal
#### Crea main.py y escribe el siguiente código:

    from kivy.app import App
    from kivy.uix.boxlayout import BoxLayout
    from kivy.uix.button import Button
    from kivy.uix.label import Label

    class MainLayout(BoxLayout):
        def __init__(self, **kwargs):
            super().__init__(**kwargs)
            self.orientation = "vertical"

            # Agregar un Label
            self.label = Label(text="¡Hola, Kivy!", font_size='24sp', size_hint=(1, 0.3))
            self.add_widget(self.label)

            # Agregar un Button
            self.button = Button(text="Presióname", size_hint=(1, 0.2))
            self.button.bind(on_press=self.on_button_press)
            self.add_widget(self.button)

        def on_button_press(self, instance):
            self.label.text = "¡Me presionaste!"

    class MiPrimeraApp(App):
        def build(self):
            return MainLayout()

    if __name__ == "__main__":
        MiPrimeraApp().run()

#### Deberías ver una ventana con un botón y un texto que cambia al presionar el botón.

#### Consejo: Usa el método Window.size para simular una resolución móvil:

    from kivy.core.window import Window

    Window.size = (360, 640)  # Simular pantalla de móvil

## Agregando un Archivo KV
#### Para separar el diseño de la lógica, usa un archivo .kv.
#### Crea un archivo llamado app.kv y añade este contenido:

    <MainLayout>:
        orientation: "vertical"
        
        Label:
            id: label
            text: "¡Hola, Kivy!"
            font_size: '24sp'
            size_hint: (1, 0.3)

        Button:
            text: "Presióname"
            size_hint: (1, 0.2)
            on_press: root.on_button_press()

#### Modifica main.py para que reconozca el archivo app.kv:

        from kivy.app import App
        from kivy.uix.boxlayout import BoxLayout

        class MainLayout(BoxLayout):
            def on_button_press(self):
                self.ids.label.text = "¡Me presionaste!"

        class MiPrimeraApp(App):
            def build(self):
                return MainLayout()

        if __name__ == "__main__":
            MiPrimeraApp().run()

## Mejoras Visuales con Kivy
#### Agregar colores
#### Usa temas de color para personalizar tu app:

    from kivy.utils import get_color_from_hex

    # Ejemplo de color:
    background_color = get_color_from_hex("#3498db")  # Azul

#### En app.kv, aplica colores:

        Button:
            background_color: 0, 0, 1, 1  # Azul con opacidad total

#### Animaciones. Kivy tiene soporte para animaciones con la clase Animation:

        from kivy.animation import Animation

        def animate_label(self):
            anim = Animation(font_size=50, duration=1) + Animation(font_size=24, duration=1)
            anim.start(self.ids.label)

## Empaquetar para Android
#### Para convertir tu aplicación en un APK, usa Buildozer.

### Instalación de Buildozer:

        pip install buildozer

### Configurar Buildozer
#### Genera un archivo de configuración:

        buildozer init

### Abre el archivo buildozer.spec y configura:

#### title: Nombre de tu app.
#### package.name: Nombre del paquete.
#### source.include_exts: Archivos que quieres incluir (como .png, .kv).

#### Genera el APK:

        buildozer -v android debug

#### Consejo: Instala Android Studio para tener configurados los SDK y NDK necesarios.

## Consejos Avanzados
#### Usa dp y sp: Para que los elementos se vean bien en diferentes resoluciones, usa unidades independientes de densidad:

        from kivy.metrics import dp, sp
        widget.size = (dp(100), dp(50))  # Ancho: 100dp, Alto: 50dp

#### Diseños Responsivos: Usa size_hint y pos_hint para diseños adaptativos:

        Button:
            size_hint: (0.8, None)
            height: dp(50)
            pos_hint: {"center_x": 0.5}

#### Depuración: Usa el log de Kivy para identificar errores:

        import kivy.logger
        kivy.logger.Logger.setLevel("DEBUG")

#### Optimización: Minimiza los recursos que cargas en tiempo de ejecución. Usa imágenes comprimidas y evita cálculos innecesarios.

