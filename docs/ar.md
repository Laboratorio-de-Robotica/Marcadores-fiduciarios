# Realidad aumentada
Esta demo de realidad aumentada superpone un modelo 3D sobre la imagen de un código QR, alineado en posición y orientación.  Para esto computa la pose del código QR como se puede ver en poseQR.py .

ARQR.py es el programa que lleva a cabo la composición completa.  Para facilitar el entendimiento se acompaña de otros dos programas que llevan a cabo demostraciones parciales de la tecnología empleada por ARQR.py.

Cada programa es autónomo, sólo requiere las bibliotecas que se mencionan en Instalación.  Los archivos se pueden mover a otra carpeta sin problemas, no están relacionados entre sí.

El documento [Realidad aumentada](https://docs.google.com/document/d/1JpMxAz1qq57-Q9i4lx_hqUtjGq__o_6Ec7lkRt19zNw/edit?usp=drive_link) profundiza en los fundamentos de la realidad aumentada y el razonamiento para este desarrollo.

La carpeta modelos dispone de algunos archivos .obj con modelos 3D.  En el código, el modelo se carga en la línea:

    triMesh = trimesh.load('modelos/fuze.obj')

Se puede modificar para usar otro modelo.

# Instalación
Las bibliotecas necesarias son las clásicas y otras dos específicas de este proyecto, necesarias para generar la vista del modelo 3D:

- OpenCV
- Numpy
- Pyrender
- Trimesh

Disponibles con PIP y también de otras maneras.

# render test.py
Esta pequeña demo genera un "render" del modelo 3D desde el punto de vista de una cámara virtual.  La pose de la cámara se determina con una matriz de 4x4, que se puede cambiar para probar otros ángulos.  Por conveniencia se proporcionan 4 poses de cámara que elegir editando código.

También produce un *mapa de profundidad*, que da idea de la tercera dimensión del modelo con una escala de colores.

# blend test.py
Esta pequeña demo va un paso más allá y combina la vista del modelo de pose fija con la imagen de la cámara.  La vista del modelo es una imagen con canal alfa, que marca los píxeles que no corresponden al modelo.

La superposición se produce en la función `blend()`, que elige pixel por pixel si toma el color del modelo o el de la imagen de cámara, logrando mostrar el modelo enfrente de la imagen.

# ARQR.py
Augmented Reality for QR codes.

Este programa adopta el código de `poseQR.py` para determinar la pose del marcador, con la que arma la pose de la cámara virtual para generar una vista del modelo, tal como se hace en `render test.py`, pero haciendo coincidir su pose con la del QR.

Finalmente se mezclan las imágenes tal como ocurre en `blend test.py`.