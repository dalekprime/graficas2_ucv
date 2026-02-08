# **Proyecto 2: Visualizador y Editor 3D Interactivo (OpenGL 3.3+)**

Este proyecto implementa un visualizador de geometría 3D robusto utilizando C++ y OpenGL Moderno (Core Profile). Permite la carga, visualización, manipulación y exportación de modelos en formato OBJ, cumpliendo con estándares de computación gráfica interactiva.

# Funcionalidades Principales

* Inicialización y Carga: Soporte completo para archivos .obj y sus materiales vinculados .mtl.
Al cargar, el modelo se escala y centra automáticamente para una visualización inicial óptima. 

* Sistema de Cámara y Navegación: Implementación de una cámara libre. Flechas para desplazarse en el plano de vista. 
Clic Derecho + Arrastrar para orientar la vista.

* Interacción y Edición: Selección de sub-mallados mediante renderizado con codificación de IDs en colores únicos.Traslación, Escala y Rotación de todo el conjunto. Al seleccionar una parte, es posible trasladarla independientemente del resto del modelo.

* Visualización Avanzada: Relleno (Fill), Alámbrico (Wireframe) y Puntos (Vertices).
Visualización de normales por vértice generadas dinámicamente, con longitud ajustable.
Visualización de caja delimitadora ajustada matemáticamente al tamaño real del sub-mallado seleccionado.
Control de Z-Buffer, Back-Face Culling y Antialiasing de líneas.

* Exportación: Capacidad de guardar el modelo modificado. La exportación aplica las matrices de transformación a los vértices y normales, generando nuevos archivos .obj y .mtl listos para usar en software externo.

# Decisiones de Diseño

* Arquitectura Monolítica: Se optó por encapsular la lógica en una clase principal C3DViewer para mantener el estado global de OpenGL y GLFW centralizado. Esto facilita la gestión del ciclo de vida de la aplicación.

* Gestión de Matrices y Normales: Se utiliza una matriz GlobalModel y una LocalModel. La posición final de un vértice es $P_{final} = M_{global} \times M_{local} \times P_{original}$.
Para soportar escalas no uniformes sin deformar la iluminación, las normales se transforman utilizando la Transpuesta de la Inversa de la matriz de modelo: $N_{final} = (M^{-1})^T \times N$.

* Escalado Diferencial: El Bounding Box se renderiza con una escala del 100.5% respecto al objeto para evitar parpadeo visual en las caras.

* Uso de Cuaterniones: Para la rotación global con el ratón, se utilizan cuaterniones en lugar de ángulos de Euler. Esto permite acumular rotaciones en ejes arbitrarios de manera suave y matemáticamente estable.

# Asunciones del Enunciado

* Se asume que el color difuso es la propiedad principal para la visualización. Propiedades como especularidad o texturas se leen pero no se renderizan, priorizando la geometría y el color base.

* Se asume que al hacer clic en el fondo, se deselecciona el sub-mallado actual y se pasa al control de rotación global del objeto.

* Se asume que los archivos .obj y .mtl se encuentran en el mismo directorio relativo al ejecutable para simplificar la carga.


# Controles

* Rotar Cámara: Clic Derecho + Arrastrar.

* Mover Cámara: Flechas Dirrecionales.

* Seleccionar: Clic Izquierdo sobre objeto.

* Rotar Objeto: Clic Izquierdo en el fondo.

* Interfaz: Mouse. Control de parámetros en panel ImGui.

# Librerías y Dependencias

* GLFW: Gestión de ventana y contexto OpenGL.

* GLAD: Carga de punteros a funciones de OpenGL (3.3 Core).

* GLM: Matemáticas para gráficos (Vectores, Matrices, Cuaterniones).

* ImGui: Interfaz gráfica de usuario inmediata.

* TinyObjLoader: Parser ligero para archivos Wavefront (.obj).

# **Autor**

*Desarrollado para la cátedra de Introducción a la Computación Gráfica. 
Universidad Central de Venezuela (UCV). Por Bryan Silva, 2026.*