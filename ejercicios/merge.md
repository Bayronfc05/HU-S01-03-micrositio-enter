# Ejercicio E5 — Provocar y resolver un conflicto de merge

**Grabación:** https://drive.google.com/drive/u/0/folders/1Ir1sLdPmkHUIFgZteFiBxu7TzR3n7_LB **Video: merge**

## Comandos usados, en orden

```bash
# 1. Crear rama de prueba
git switch -c prueba-conflicto

# 2. Cambiar el <h1> de index.html en esta rama
git add index.html
git commit -m "test: cambio de titulo en rama prueba-conflicto"

# 3. Volver a main
git switch main

# 4. Cambiar el mismo <h1>, pero con texto distinto
git add index.html
git commit -m "test: cambio distinto de titulo en main"

# 5. Intentar mergear -> esto provoca el conflicto
git merge prueba-conflicto
# Salida: CONFLICT (content): Merge conflict in index.html

# 6. Abrir index.html y ver las marcas de conflicto:
#    <<<<<<< HEAD
#    <h1>De Enter a la pantalla: el recorrido completo</h1>
#    =======
#    <h1>El viaje de una petición web</h1>
#    >>>>>>> prueba-conflicto

# 7. Edité el archivo para quedarme con un solo título
#    (en mi caso, terminé conservando el de la rama: "El viaje de una petición web")
git add index.html
git commit -m "fix: resuelve conflicto de merge en index.html"

# 8. Limpieza: borrar la rama de prueba
git branch -d prueba-conflicto
```

## Qué aprendí

- Un conflicto de merge pasa cuando dos ramas modifican la **misma línea** de un archivo
  de forma distinta, y Git no puede decidir solo cuál dejar.
- Git marca el conflicto con `<<<<<<<`, `=======` y `>>>>>>>` directamente en el archivo.
- **Error real que cometí:** la primera vez que "resolví" el conflicto, dejé sin querer
  una marca de conflicto suelta (no borré todas las líneas de `<<<<<<<`/`=======`/`>>>>>>>`).
  Git **no valida que el archivo quede coherente** — solo te deja hacer commit si corriste
  `git add`, sin importar si el contenido tiene basura adentro. Me di cuenta al revisar
  `git log --oneline --graph`, porque vi un commit extra con mensaje raro, y confirmé el
  problema con `git --no-pager show <hash> -- index.html`.
- Corregí el archivo, hice un nuevo commit con mensaje claro, y confirmé con
  `grep "<h1>" index.html` que ya no quedaba ninguna marca.
- **Conclusión:** siempre hay que revisar el archivo completo después de resolver un
  conflicto, no solo confiar en que "ya guardé" — Git no te avisa si dejaste basura.