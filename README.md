# Patitas ID
**Proyecto integrador · Fase 2 · Herramientas de procesamiento para IA · IN1050-A4-mascotas**
Este proyecto busca ayudar a las personas que han perdido a sus perros o que han encontrado uno y desean saber si podría pertenecer a alguien. Para ello, se desarrolla un sistema basado en inteligencia artificial capaz de comparar dos fotografías de perros y analizar qué tan similares son visualmente. El sistema utiliza un modelo especializado en identificación individual de animales para extraer características de las imágenes y calcular un valor de similitud. De esta manera, se busca ofrecer una herramienta tecnológica que facilite la búsqueda y recuperación de mascotas, apoyando a sus dueños y a las personas que participan en el rescate y cuidado de animales.

## Equipo
|Nombre completo|Rol de equipo|Ficha individual|
|---|---|---|
|Pablo Israel Avalos Moreno|Encargado del README principal del equipo|[Ficha](equipo/Pablo.md) |
|Hector Ulises Serrano Ramos|Encargado de asignación y control del modelo|[Ficha](equipo/Hector.md) |
|Jessica Abigail Tovar Solis|Encargada de la parte creativa y visual|[Ficha](equipo/abigail.md) |

## Problemática
La pérdida de mascotas es una situación que afecta a muchas familias y encontrar a un perro puede resultar complicado cuando no se cuenta con información suficiente para identificarlo. En ocasiones, las personas publican fotografías de perros encontrados o buscan a sus mascotas mediante redes sociales, pero comparar visualmente las imágenes puede ser difícil, especialmente cuando existen diferencias de iluminación, posición, distancia o calidad fotográfica. Por esta razón, nuestro proyecto propone utilizar inteligencia artificial para analizar las características visuales de los perros y determinar si dos fotografías podrían corresponder al mismo animal. [Investigación de la problemática](docs/investigación.md)

## Caso de uso
El usuario principal es una persona que ha perdido a su perro o que ha encontrado uno y desea comprobar si podría tratarse de la misma mascota.

El funcionamiento contempla los siguientes elementos:
- **Entrada:** el usuario proporciona dos fotografías de perros que desea comparar.
- **Procesamiento:** el sistema analiza ambas imágenes mediante un modelo especializado en identificación individual de animales.
- **Resultado:** se obtiene un valor de similitud que permite conocer qué tan parecidas son las características visuales de ambos perros.
- **Interpretación:** con base en el resultado, el sistema ofrece una orientación sobre la posibilidad de que las fotografías correspondan al mismo perro.

> El resultado funciona como una referencia para apoyar la búsqueda, no como una confirmación definitiva de identidad.

## Modelo
|Dato|Respuesta|
|---|---|
|Identificador|[AvitoTech/DINO-v2-small-for-animal-identification](https://www.google.com/url?q=https%3A%2F%2Fhuggingface.co%2FAvitoTech%2FSigLIP2-Base-for-animal-identification)|
|Tarea (pipeline tag)|`image-feature-extraction (Extracción de Embeddings para Re identificación)`|
|Número de parámetros| 22,000,000|
|Licencia|Apache 2.0 |
|Limitación o sesgo declarado| Disminución en la precisión de identificación cuando las fotografías presentan iluminación deficiente, ángulos muy inclinados o cuando el rostro/cuerpo de la mascota se encuentra parcialmente ocluido.|


## Como funciona
```mermaid
flowchart TD
    A([Inicio]) --> B[/Usuario ingresa 2 imágenes/]
    B --> |Fotografías digitales| C[Modelo DINOv2]
    C --> D[Extracción de características]
    D --> |Vectores de rasgos| E[Comparación de embeddings]
    E --> F[Cálculo de similitud coseno]
    F --> G{Resultado de similitud}
    G --> |Coincidencia válida| H([Posible coincidencia del perro/gato])
	G --> |Sin coincidencias| I[Solicitar nueva fotografia]
	I --> |Reintento| B
```
## Infraestructura

Memoria mínima=N×2 bytes≈ ? GB

$$
\text{Memoria mínima} = N \times 4\ \text{bytes} \approx \ ?\ \text{GB}
$$

$$
\text{Memoria mínima} = 22,100,000 \times 4\ \text{bytes} \approx 88,400,000\ \text{bytes}
$$


- **VRAM disponible en Colab:** 14  GB (GPU-T4)
- **Dónde se ejecuta:** Colab on GPU
- **Por qué:** Se ejecutará en Google Colab con GPU. El modelo requiere únicamente ~88.4 MB, lo que representa menos del 5% de la VRAM asignada por Colab. Esto garantiza una inferencia rápida y local sin exceder los recursos del entorno gratuito ni depender de cuotas de una API externa.

## Riesgo ético

- **Riesgo:** Posible error en la comparación de imágenes, y a futuro, pueden existir riesgos mayores debido al uso de datos personales. 
- **Mitigación:** Para nuestro riesgo actual (comparación falsa) podemos definir de manera más precisa los parámetros de las comparaciones. 


##  Cambios respecto a la Fase 1

1. Cambio en el enfoque del proyecto: Decidimos modificar el enfoque inicial del proyecto, ya que todavía no teníamos completamente definido qué dirección queríamos seguir. Por ello, ajustamos la idea para tener objetivos más claros.

2. Redistribución de roles: Modificamos ligeramente las responsabilidades de cada integrante, sin cambiar por completo los roles originales, con la intención de fomentar un mayor apoyo y colaboración entre todos.

3. Modificación en los resultados del modelo: Cambiamos la manera en que el modelo presenta los resultados. En lugar de mostrar únicamente un «sí» o un «no» al comparar las imágenes, ahora proporciona un porcentaje de probabilidad del 0 al 100 % sobre la similitud entre ambas imágenes.

## Siguientes Pasos
- [ ] Seguir haciendo pruebas ,ahora con un caso real para probar la certania de nuestro modelo
- [ ] Aprender nuevas herramientas y aplicarlas (interfaz,mas sobre hit gub, etc)
- [ ] Mejorar en aspectos de la terminal y GitHub

## Referencias
1. [AvitoTech. (2024). DINO-v2-small-for-animal-identification Model Card. Hugging Face Repository.](https://huggingface.co/AvitoTech/DINO-v2-small-for-animal-identification)
2. [Papa León XIV. (2026). Carta Encíclica Magnífica Humanitas: Sobre la custodia de la persona humana en el tiempo de la inteligencia artificial. La Santa Sede.](https://www.vatican.va/content/leo-xiv/es/encyclicals/documents/20260515-magnifica-humanitas.html)
3. [Instituto Nacional de Estadística y Geografía (INEGI). (2021). Encuesta Nacional de Bienestar Autorreportado (ENBIARE) 2021: Módulo de Mascotas y Animales de Compañía. INEGI México.](https://www.inegi.org.mx/programas/enbiare/2021/)
