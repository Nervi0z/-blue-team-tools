# Contributing

Contribuciones bienvenidas: nuevas herramientas, correcciones, enlaces rotos, entradas desactualizadas y ajustes de formato.

---

## Formas de contribuir

- **Nueva herramienta:** Abre un [issue](https://github.com/Nervi0z/blue-team-tools/issues/new?template=add-tool.md) con el nombre, enlace y un apunte sobre su uso defensivo concreto
- **Corregir entrada existente:** Enlace roto, información desactualizada, descripción mejorable — abre un pull request directamente
- **Typos y formato:** PRs pequeños sin issue previo son aceptables
- **Errores en la estructura:** Abre un issue

---

## Proceso para un pull request

1. Fork del repositorio
2. Clona tu fork:
   ```bash
   git clone https://github.com/TU_USUARIO/blue-team-tools.git
   ```
3. Crea una rama descriptiva:
   ```bash
   git checkout -b add-velociraptor-endpoint
   git checkout -b fix-zeek-broken-link
   ```
4. Edita el archivo `.md` correspondiente en `tools/`
5. Commit con prefijo [Conventional Commits](https://www.conventionalcommits.org/):
   ```bash
   git commit -m "feat: add Velociraptor to endpoint section"
   git commit -m "fix: update broken Zeek documentation link"
   git commit -m "docs: correct OpenSSL enc example"
   ```
6. Push de la rama:
   ```bash
   git push origin tu-rama
   ```
7. Abre un pull request contra `main`. Referencia el issue relacionado con `Closes #NUMERO` si aplica

---

## Formato de entrada

Usa esta estructura para todas las entradas nuevas en `tools/*.md`:

```markdown
## Nombre de la herramienta

- **Description:** Qué hace, enfocado en el uso defensivo.
- **Blue Team use:**
  - Caso de uso concreto 1
  - Caso de uso concreto 2
- **Website:** [url](https://...)
- **Type:** CLI / GUI / Web service / Framework / Platform
- **Platform:** Linux / Windows / macOS / Web
- **Installation:**
  ```bash
  sudo apt install herramienta
  ```
- **Usage examples:**
  ```bash
  # Ejemplo real con comentario explicativo
  herramienta --flag valor
  ```
- **Alternatives:** Herramienta1, Herramienta2
- **Notes:** Notas de configuración, advertencias, consejo específico de Blue Team.
```

Criterios de calidad:

- Descripciones concretas y enfocadas en uso defensivo — sin frases genéricas
- Todos los enlaces verificados antes de enviar
- Preferencia por herramientas open source y mantenidas activamente
- Comandos reales y ejecutables, no descripciones de lo que hace un comando
- Una entrada bien documentada vale más que tres incompletas
