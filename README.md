<div align="center">

# FORM-IC-01

**Investigación individual: arquitecturas distribuidas en la industria**

![UTEQ](https://img.shields.io/badge/UTEQ-Ingenier%C3%ADa%20de%20Software-1f6feb?style=flat-square)
![Asignatura](https://img.shields.io/badge/Aplicaciones%20Distribuidas-ISR--701-8957e5?style=flat-square)
![Microservicios](https://img.shields.io/badge/Estilo-Microservicios-e36209?style=flat-square)
![LaTeX](https://img.shields.io/badge/LaTeX-pdflatex%20%2B%20biber-008080?style=flat-square&logo=latex&logoColor=white)

</div>

---

Séptimo nivel, paralelo A · SPA 2026-2027 · Actividad formativa individual que prepara el informe TA-IND-02. Analiza la migración de SoundCloud, de un monolito a una arquitectura de microservicios.

Autor: Eduardo David Reinoso Vélez (ereinosov@uteq.edu.ec)

Docente: Gleiston Cicerón Guerrero Ulloa, PhD

Cierre: sábado 28 de noviembre de 2026, 23:59

Repositorio: https://github.com/ereinosov/app-dist-form-ic-01

## Estructura

```
app-dist-form-ic-01/
├── main.tex          # Archivo principal del informe
├── referencias.bib   # Referencias en formato IEEE (biblatex)
├── main.pdf          # PDF compilado
├── capturas/         # Captura anotada de la fuente principal
├── .gitignore
└── README.md
```

## Compilación

Requisitos: MiKTeX o TeX Live con `pdflatex` y `biber`. Entorno usado: Windows, MiKTeX 25.12, TeXstudio.

Desde la carpeta raíz del repositorio, ejecutar en este orden:

```
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

El resultado es `main.pdf`. Los paquetes que carga `main.tex` se instalan solos en MiKTeX; en TeX Live deben estar instalados.
