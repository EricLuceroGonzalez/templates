# templates

Plantillas para empezar proyectos y completar repos existentes.

| Carpeta | Para qué | Cómo se usa |
| --- | --- | --- |
| `python/` | Proyecto Python con uv, ruff, pytest y Makefile. Variante "investigación" con `data/`, `notebooks/`, `results/` y `CITATION.cff` | `nuevo python <contexto>/<nombre>` |
| `latex-article/` | Artículo o informe: biblatex + biber, latexmk con auxiliares en `build/` | `nuevo latex-article <contexto>/<nombre>` |
| `latex-beamer/` | Presentación Beamer (metropolis, Madrid o default; 16:9 o 4:3) | `nuevo latex-beamer <contexto>/<nombre>` |
| `_baseline/` | Archivos base (`.gitignore` por tipo, README, LICENSE) para repos viejos | `completar-repo.sh` |

## Crear un proyecto

Con la función `nuevo` de los dotfiles (crea el proyecto, hace `git init` y el primer commit):

```bash
nuevo python personal/analisis-encuestas
nuevo latex-beamer phd/2026-11-seminario-alns
```

O directamente con copier:

```bash
uvx copier copy ~/Developer/tools/templates/python ~/Developer/personal/analisis-encuestas
```

Copier hace unas preguntas (nombre, descripción, licencia...) y genera los archivos.

## Actualizar un proyecto cuando mejora la plantilla

Cada proyecto guarda sus respuestas en `.copier-answers.yml`. Tras hacer commit de los cambios en la plantilla:

```bash
cd <proyecto>
uvx copier update      # aplica las mejoras; si hay conflictos, los marca como en un merge
```

## Editar una plantilla

- Las preguntas están en `copier.yml`; los archivos, en `template/`.
- Los archivos terminados en `.jinja` se rellenan con las respuestas (`{{ project_name }}`); el resto se copia tal cual.
- Una carpeta o archivo cuyo nombre es `{% if ... %}nombre{% endif %}` solo se crea si se cumple la condición.
- Prueba sin preguntas: `uvx copier copy --defaults --data project_name=prueba python /tmp/prueba`.
- Haz commit de la plantilla antes de usarla: copier toma la última versión guardada en Git.
