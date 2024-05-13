# 🏥 **My_Health_App** 

📝 **Descripción**

🌐 **My_Health_App**  es una aplicación una aplicación móvil desarrollada con Flutter que te proporciona varias herramientas útiles:
**1). Calculadora de Edad:** Simplemente ingresa tu fecha de nacimiento y la aplicación te mostrará tu edad actual.
**2). Calculadora de Índice de Masa Corporal (IMC):** Ingresa tu peso y altura, y la aplicación calculará tu IMC, ofreciéndote una indicación de tu salud en relación con tu altura.
**3). Buscador de Signo Zodiacal:** Introduce tu fecha de nacimiento y la aplicación te revelará tu signo zodiacal según la astrología occidental.

# 📦 **Cómo Desplegar**

**Prerrequisitos**

<img src="https://github.com/Stephanie4712205/My_Health_App/assets/161189108/5f3ed1eb-148b-4d33-845f-f54ed4413aa7" alt="Texto alternativo" width="30"/> vysor instalado (En el pc y el celular)


# 🔧 **Configuración de la Aplicación**

*  En visual studio code seleccionamos **ctrl + shift + p**
*  Seleccionamos **New Project**
*  Seleccionamos **Empty Application**
*  Seleccionamos carpeta

  # 🚀 Despliegue

  * **Main**
este código crea una aplicación Flutter con un enrutador declarativo que gestiona las rutas de la aplicación, y la configuración de las rutas se define en otro lugar.

**Ejemplo:**

```import 'package:flutter/material.dart';
import 'package:my_health_app/src/feature/screens/age_screen.dart';
import 'package:my_health_app/src/feature/screens/bmi_screen.dart';
import 'package:my_health_app/src/routes/my_health_app_router.dart';

void main() {
  runApp(MainApp());
}

class MainApp extends StatelessWidget {
   MainApp({super.key});

  @override
  Widget build(BuildContext context) {
    return  MaterialApp.router(
      routerConfig: MyHealthAppRouter.router,
      debugShowCheckedModeBanner: false,
    );
  }
}
```

* **Screens**
contener los archivos de código relacionados con las diferentes pantallas o vistas de la aplicación. Cada archivo en esta carpeta generalmente representa una pantalla específica de la interfaz de usuario que el usuario final verá y con la que interactuará.

** Ejemplo:**

```
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';
import 'package:my_health_app/src/feature/widgets/my_health_app_drawer.dart';

class AgeScreen extends  StatefulWidget
{
  @override
  _ageScreenState createState()=> _ageScreenState();
}

class _ageScreenState extends State<AgeScreen> 
{
  DateTime? _selectedDate;
  int? _age;

  void _presentDatePicker(){
    showDatePicker(
      context: context,
      initialDate: DateTime.now(), 
      firstDate: DateTime(1900), 
      lastDate: DateTime.now(),
    ).then ((pickedDate){
      if (pickedDate == null) return;
      setState(() {
        _selectedDate = pickedDate;
        _age = _calculateAge(pickedDate);
      });
    });
  }

  int _calculateAge(DateTime birthDate)
  {
    DateTime currentDate = DateTime.now();
    int age = currentDate.year - birthDate.year;
    if (currentDate.month < birthDate.month || 
      (currentDate.month == birthDate.month)) {
        age--;
      }
      return age;
  }

  @override
  Widget build (BuildContext context)
  {
    return Scaffold(
      drawer: MyHealthAppDrawer(),
      appBar: AppBar(
        title: Text('Age Calculator'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            ElevatedButton(
              onPressed: _presentDatePicker,
              child: Text(_selectedDate == null
              ? 'Select your birthdate'
              : 'Change birthdate(${_selectedDate?.toIso8601String().substring(0, 10)})'),
               style: ElevatedButton.styleFrom(
                backgroundColor: Colors.pink,
                foregroundColor: Colors.white,
                padding: EdgeInsets.symmetric(horizontal:30, vertical: 15)),
            ),
            SizedBox(height:20),
            if(_age != null)
              Text('You are $_age years old.' , style: TextStyle (fontSize: 18)),
          ],
        ),
      ),
    );
  }

}
```

* **Widgets**

Son los bloques de construcción fundamentales en Flutter que se utilizan para construir la interfaz de usuario de una aplicación, y comprenden una variedad de componentes visuales y de comportamiento que se pueden combinar para crear interfaces de usuario complejas y ricas.

**Ejemplo:**

```
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

class MyHealthAppDrawer extends StatelessWidget
{
  @override
  Widget build(BuildContext context)
  {
    return Drawer(
      child: ListView(
        children: <Widget>[
          DrawerHeader(
            child: Text('My Health App'),
            decoration: BoxDecoration(
              color: Colors.pink,
            ),
          ),
          ListTile(
            title: Text('Home'),
            onTap: () {
              Navigator.pop(context);
              context.go('/');
            },
          ),
          ListTile(
            title: Text('BMI Calculator'),
            onTap: () {
              Navigator.pop(context);
              context.go('/bmi');
            },
          ),
          ListTile(
            title: Text('Age Calculator'),
            onTap: () {
              Navigator.pop(context);
              context.go('/age');
            },
          ),
          ListTile(
            title: Text('Zodiac Calculator'),
            onTap: () {
              Navigator.pop(context);
              context.go('/zodiac');
            },
          ),
        ],
      ),
    );
  }
}
```

* **Routes**
  
son importantes para la navegación dentro de la aplicación y se definen en el nivel más alto de la jerarquía de widgets. Permiten a los usuarios moverse entre diferentes pantallas y gestionar la interacción de la aplicación de manera efectiva.

**Ejemplo:**

```
import 'package:go_router/go_router.dart';
import 'package:my_health_app/src/feature/screens/age_screen.dart';
import 'package:my_health_app/src/feature/screens/bmi_screen.dart';
import 'package:my_health_app/src/feature/screens/home_screen.dart';
import 'package:my_health_app/src/feature/screens/zodiac_screen.dart';

class MyHealthAppRouter
{
  static GoRouter router = GoRouter(routes: [
    GoRoute(path: '/', builder: ((context, state) => HomeScreen())),
    GoRoute(path: '/bmi', builder: ((context, state) => BmiScreen())),
    GoRoute(path: '/age', builder: ((context, state) => AgeScreen())),
    GoRoute(path: '/zodiac', builder: ((context, state) => ZodiacScreen())),
  ]);
}
```
