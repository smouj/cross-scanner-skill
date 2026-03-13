description: Escáner impulsado por IA para tareas de escritura
version: 1.0.0
tags: escritura, ia, automatización
author: SMOUJ
date: 2026-03-13
---

# Habilidad de Escáner Cruzado

## Propósito

El Escáner Cruzado es una herramienta avanzada impulsada por IA integrada en OpenClaw, específicamente diseñada para analizar y mejorar contenido escrito en diversos dominios. Utiliza procesamiento de lenguaje natural y modelos de aprendizaje automático para proporcionar retroalimentación integral sobre la calidad de la escritura, incluyendo correcciones gramaticales, mejoras de estilo, mejoras de legibilidad y sugerencias de optimización de contenido.

### Casos de Uso Reales

- **Optimización de Contenido de Blog**: Escanear publicaciones de blog para palabras clave SEO, puntuaciones de legibilidad (usando Flesch-Kincaid) y métricas de engagement para mejorar la visibilidad en línea y la retención de usuarios.
- **Revisión de Documentación Técnica**: Analizar docs de API, manuales de usuario o comentarios de código para claridad, consistencia y precisión técnica, asegurando que cumplan con estándares de la industria como ISO/IEC 18004.
- **Mejora de Escritura Creativa**: Revisar novelas, cuentos cortos o guiones para flujo narrativo, desarrollo de personajes, coherencia de trama y elementos estilísticos como uso de metáforas y ritmo.
- **Auditoría de Comunicación Profesional**: Revisar correos electrónicos comerciales, informes o presentaciones para adecuación de tono, detección de sesgos y sensibilidad cultural para mantener la imagen corporativa.
- **Análisis de Artículos Académicos**: Evaluar papers de investigación para integridad de citas, fuerza argumental y adherencia a convenciones de escritura académica (estilos APA, MLA, Chicago).
- **Refinamiento de Copia de Marketing**: Optimizar copias publicitarias, descripciones de productos o publicaciones en redes sociales para lenguaje persuasivo, efectividad de llamadas a la acción y segmentación de audiencia.

## Alcance

### Comandos Específicos

El Escáner Cruzado opera a través de un conjunto de comandos CLI accesibles vía la interfaz de OpenClaw:

- `openclaw cross-scanner scan-text --input \"text here\" --mode grammar`: Escanea texto proporcionado en busca de errores gramaticales y correcciones básicas.
- `openclaw cross-scanner scan-file --path /path/to/file.md --output report.json`: Analiza un archivo y genera un informe detallado en JSON.
- `openclaw cross-scanner suggest-improvements --content \"text\" --focus readability`: Proporciona sugerencias específicas para mejorar aspectos como legibilidad o SEO.
- `openclaw cross-scanner generate-summary --file /path/to/document.txt --length short`: Crea un resumen conciso del contenido escaneado.
- `openclaw cross-scanner compare-versions --original file1.txt --revised file2.txt`: Compara dos versiones de texto y resalta diferencias con puntuaciones de mejora.
- `openclaw cross-scanner batch-scan --directory /path/to/folder --filter \"*.md\"`: Procesa múltiples archivos en un directorio con filtrado de comodines.

### Variables de Entorno

- `CROSS_SCANNER_API_KEY`: Clave API requerida para acceder a modelos de IA (ej. OpenAI GPT-4 o similar). Establecer vía `export CROSS_SCANNER_API_KEY=your_key_here`.
- `CROSS_SCANNER_MODEL`: Selección opcional de modelo (predeterminado: \"gpt-4\"). Opciones incluyen \"claude-3\" o \"llama-3\".
- `CROSS_SCANNER_TIMEOUT`: Tiempo máximo de procesamiento en segundos (predeterminado: 30).
- `CROSS_SCANNER_LANGUAGE`: Idioma objetivo para análisis (predeterminado: \"en\"). Soporta códigos de idioma ISO como \"es\" para español.

### Dependencias y Requisitos

- **Requisitos del Sistema**: Linux/macOS/Windows con Python 3.8+, Node.js 16+ para integración.
- **Dependencias**: Instalar vía `pip install openai langchain nltk spacy`. Requiere modelos de `spacy`: `python -m spacy download en_core_web_sm`.
- **Acceso a API**: Suscripción válida a proveedores de IA soportados (OpenAI, Anthropic o modelos locales vía Ollama).
- **Almacenamiento**: Mínimo 1GB de espacio en disco libre para informes temporales y análisis en caché.

## Proceso de Trabajo Detallado

1. **Validación de Entrada**: Verificar que el texto/archivo de entrada exista y cumpla con límites de tamaño (máx. 10MB por archivo, 50,000 caracteres para texto directo).
2. **Preprocesamiento**: Tokenizar texto usando NLTK, detectar idioma con langdetect y aplicar filtrado básico para reducción de ruido.
3. **Análisis de IA**: Enviar contenido procesado al modelo de IA seleccionado con prompts específicos (ej. \"Analiza este post de blog para SEO y sugiere mejoras\").
4. **Generación de Retroalimentación**: Recibir respuesta del modelo, analizar en categorías (gramática, estilo, contenido, SEO) y puntuar cada aspecto en una escala de 0-100.
5. **Formateo de Salida**: Generar informe legible por humanos con sugerencias en línea, resaltados coloreados (rojo para errores, amarillo para advertencias, verde para positivos) y opciones de exportación (JSON, Markdown, PDF).
6. **Interacción con Usuario**: Permitir modo interactivo donde los usuarios pueden aceptar/rechazar sugerencias vía prompts de CLI.
7. **Registro y Métricas**: Registrar tiempo de análisis, uso de tokens y métricas de precisión para mejora continua.

### Pasos de Verificación

- **Verificación Post-Escaneo**: Ejecutar `openclaw cross-scanner verify --report report.json` para validar integridad del informe y referenciar cruzadamente con contenido original.
- **Prueba de Precisión**: Comparar sugerencias de IA contra corrección manual para un conjunto de muestra; apuntar a >85% de acuerdo.
- **Benchmark de Rendimiento**: Asegurar tiempo promedio de escaneo <5 segundos para <1000 palabras usando `time openclaw cross-scanner scan-text --input \"sample text\"`.
- **Prueba de Integración**: Confirmar que la salida se integre con el editor de archivos de OpenClaw sin conflictos.

## Reglas de Oro

1. **Preservar Autenticidad**: Nunca alterar el mensaje central o la voz única del autor; las sugerencias deben mejorar, no reemplazar.
2. **Uso Ético de IA**: Evitar sugerencias sesgadas; usar datos de entrenamiento diversos e implementar verificaciones de equidad.
3. **Privacidad Primero**: Procesar contenido localmente cuando sea posible; nunca transmitir datos sensibles sin consentimiento explícito.
4. **Retroalimentación Accionable**: Cada sugerencia debe incluir por qué se recomienda y cómo implementarla.
5. **Conciencia de Contexto**: Adaptar análisis basado en tipo de contenido (ej. formal para informes, creativo para ficción).
6. **Aprendizaje Continuo**: Incorporar retroalimentación de usuarios para refinar prompts de IA y mejorar escaneos futuros.
7. **Eficiencia de Recursos**: Limitar llamadas a API para prevenir overuse; cachear análisis frecuentes para contenido repetido.

## Ejemplos

### Ejemplo 1: Escaneo Básico de Gramática
**Comando de Entrada**: `openclaw cross-scanner scan-text --input \"This is a example sentance with to many erros.\"`

**Salida**:
```
Escaneo completado en 2.3 segundos.

Original: \"This is a example sentance with to many erros.\"
Corregido: \"This is an example sentence with too many errors.\"

Sugerencias:
- Gramática: Cambiado \"a\" a \"an\" (regla de artículo indefinido).
- Ortografía: \"sentance\" → \"sentence\", \"erros\" → \"errors\".
- Estilo: \"to many\" → \"too many\" (corrección de cuantificador).

Puntuación: Gramática: 75/100 | Legibilidad: 82/100
```

### Ejemplo 2: Análisis de Archivo con Enfoque en SEO
**Comando de Entrada**: `openclaw cross-scanner scan-file --path /home/user/blog-post.md --focus seo --output seo-report.json`

**Salida** (extracto):
```
Archivo: /home/user/blog-post.md (1245 palabras)

Análisis SEO:
- Densidad de Palabras Clave: \"machine learning\" aparece 8 veces (rango óptimo: 1-2%).
- Descripción Meta: Faltante; Sugerencia: \"Explora lo último en técnicas de machine learning para científicos de datos.\"
- Legibilidad: Puntuación Flesch: 68 (apuntar a 60-70).
- Sugerencias: Agregar enlaces internos a posts relacionados, optimizar etiquetas H1/H2.

Informe completo guardado en seo-report.json.
```

### Ejemplo 3: Revisión de Escritura Creativa
**Comando de Entrada**: `openclaw cross-scanner suggest-improvements --content \"The hero walked slowly into the dark forest, his heart pounding.\" --mode creative`

**Salida**:
```
Mejoras Creativas:
- Detalle Sensorial: Agregar descripciones (ej. \"El crujido de las hojas bajo sus pies hacía eco con su corazón palpitante\").
- Ritmo: Considerar dividir en oraciones más cortas para tensión.
- Metáfora: \"Su corazón palpitaba como un tambor de guerra\" podría aumentar el drama.

Tono General: Suspenseful, pero podría ser más inmersivo.
```

## Comandos de Reversión

- **Deshacer Cambio Único**: `openclaw cross-scanner undo --report report.json --change-id 3` (revierte sugerencia específica por ID).
- **Revertir Archivo**: `openclaw cross-scanner revert-file --original /path/to/original.txt --modified /path/to/modified.txt` (sobrescribe modificado con original).
- **Limpiar Caché**: `openclaw cross-scanner clear-cache` (elimina todos los análisis en caché para comenzar de nuevo).
- **Reiniciar Sesión**: `openclaw cross-scanner reset` (limpia datos de sesión actual y preferencias).

## Solución de Problemas

### Problemas Comunes
- **Límite de Tasa de API**: Error \"429 Too Many Requests\". Solución: Aumentar `CROSS_SCANNER_TIMEOUT` o cambiar a un modelo diferente.
- **Error de Archivo Grande**: \"File exceeds size limit\". Solución: Dividir archivo en fragmentos usando `split -l 1000 file.txt chunk_` luego escanear en lote.
- **Fallo en Detección de Idioma**: Salida muestra \"Unknown Language\". Solución: Establecer manualmente `CROSS_SCANNER_LANGUAGE=es` para contenido no inglés.
- **Sugerencias Inexactas**: Puntuaciones bajas en verificación. Solución: Actualizar modelo de IA vía `pip install --upgrade openai` o cambiar proveedores.
- **Errores de Tiempo de Espera**: Proceso se cuelga. Solución: Reducir longitud de contenido o aumentar timeout; verificar conectividad de red.

### Registros y Depuración
- Habilitar modo verboso: Agregar flag `--verbose` a cualquier comando.
- Verificar registros: `tail -f /home/smouj/.openclaw/logs/cross-scanner.log`
- Reportar bugs: Usar `openclaw feedback --skill cross-scanner --issue \"description\"` para enviar a desarrolladores.