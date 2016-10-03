# Respuestas al Ejercicio 1 de la Práctica de Git

1. **¿Qué comando utilizaste en el paso 11? ¿Por qué?**

Para el paso 11 usé el comando `git reset --hard HEAD~1`. 
Con el comando `git reset` muevo el puntero de la rama *styed* al commit deseado, que en este caso era el commit anterior al realizado en el paso 10 (se referencia en este caso usando una posición relativa al commit en el que nos encontramos en el paso 11 con `HEAD~1`).
Por defecto, el comando `git reset` conserva los ficheros ubicados en el *working copy* que estuvieran en el momento de ser ejecutado. Para eliminar estos ficheros se ha añadido la opción `--hard`.

2. **¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**

En este caso usé el comando `git reset --hard HEAD@{1}`.
Como git no elimina ningún commit del repositorio, lo único que se necesitaba era volver a mover el puntero de la rama *styled* para que volviera a apuntar al commit al que habíamos dejado de tener acceso en el paso 11.
Puesto que entre los pasos 11 y 12 no se ha realizado ninguna acción adicional a la que se describe en el enunciado de la práctica, podemos acceder al commit anterior con la referencia `HEAD@{1}`, que indica el último commit en el que nos encontrábamos antes de estar en el commit actual.

3. **El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

El merge del paso 13 no realizó ninguna modificación en el repositorio.
Al estar en la rama *styled* y ejecutar el comando `git merge master`, se obtuvo la siguiente salida por pantalla:
`Already up-to-date.`
Si se piensa detenidamente, esta respuesta tiene mucho sentido, porque al querer tener acceso desde la rama *styled* a todos los commits de la rama *master*, git nos responde que esta rama ya tiene acceso a todos los commits de *master* (de hecho, la rama *styled* tiene todos los commits de *master*, más el commit que se generó en el paso 10).

4. **El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?**

Sí. El merge del paso 19 causó conflictos porque ambas ramas que se querían combinar modifican las mismas líneas en el fichero *git-nuestro.md*.

5. **El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?**

No. El merge efectuado en este paso sólo requería actualizar el puntero de la rama *master* a la posición donde apunta el puntero de la rama *styled*. Por lo tanto, este merge es de tipo *fast-forward* y no requiere realizar commits adicionales, y por este motivo no puede generar conflictos.

6. **¿Qué comando o comandos utilizaste en el paso 25?**

He usado el comando `git log --graph --decorate --pretty=oneline`.

Con el comando `git log` listo todos los commits de mi rama actual. Al añadir la opción `--graph`, muestra una representación gráfica de las relaciones entre los commits listados, y la opción `--decorate` muestra los nombres de todos los punteros que contiene el repositorio (es decir, el puntero *HEAD*, etiquetas y ramas locales y remotas). Por último, con la opción `--pretty=oneline` estamos especificando que sólo se muestre el resumen textual de cada commit en una línea.

7. **El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

Sí. La rama *title* tan sólo contenía un commit adicional a los commits de la rama *master*, cuyo padre era el último commit al que apuntaba la rama *master*.

8. **¿Qué comando o comandos utilizaste en el paso 27?**

Usé el comando `git reset HEAD~1`. De esta forma muevo el puntero de la rama *master* al anterior commit al que apuntaba mientras que conservo los cambios en el *working copy* (por eso no se emplea la opción `--hard`).

9. **¿Qué comando o comandos utilizaste en el paso 28?**

Para este paso utilicé el comando `git checkout -- git-nuestro.md`, que es el comando que git sugiere cuando se ejecuta el comando `git status`.

10. **¿Qué comando o comandos utilizaste en el paso 29?**

Usé el comando `git branch -D title`. En este caso no se podía emplear la opción `-d`, puesto que al eliminar la rama *title* hemos perdido una referencia al último commit que contenía esta rama.

11. **¿Qué comando o comandos utilizaste en el paso 30?**

Para resolver este paso he usado el comando `git reset --hard HEAD@{1}`. Podría haber utilizado el comando `git reflog` para averiguar el *commit-ID* del commit del anterior merge, pero en este caso concreto, al no habernos movido de commit desde que deshicimos el merge en el paso 27, podemos inferir que el commit al que queremos mover la rama *master* es justo el anterior commit en el que nos encontrábamos. 

12. **¿Qué comando o comandos usaste en el paso 32?**

En este punto he usado el comando `git checkout $(git rev-list --max-parents=0 HEAD)`. A juzgar por lo que he leído del paso 32, he interpretado que no se exigía mover el puntero de la rama *master*. En caso contrario, hubiera usado el comando `git reset --hard $(git rev-list --max-parents=0 HEAD)`.

**NOTA:** Para resolver este paso me he permitido buscar en la documentación de git para encontrar una forma de volver al commit inicial de un repositorio empleando una sola línea de código. He creído conveniente esta acción para permitirme conocer mejor los entresijos de esta herramienta.

Debo decir que esta solución logra lo que se propone empleando una sóla línea, pero no un único comando: en realidad, lo que está sucediendo es que estoy ejecutando el comando `git checkout` y le estoy pasando como referencia al commit el resultado de ejecutar el comando `git rev-list --max-parents=0 HEAD`.

El comando `git rev-list <commitID>` lista todos los *hashes* de los commits accesibles desde el commit <commitID>, es decir, sería equivalente a ejecutar un `git log`, pero sólo mostrando los *hashes* de los commits. Además, al usar la opción `--max-parents=0` estoy filtrando la lista de resultados que me ejecuta el comando, limitando los resultados a los *hashes* de aquellos commits que no tienen ningún padre y por tanto, muestro sólo el *hash* del commit inicial del repositorio. 

13. **¿Qué comando o comandos usaste en el punto 33?**

En este paso, teniendo en cuenta que en el paso anterior realicé un `git checkout`, he usado el comando `git checkout master`.

He de reconocer que en este caso era más sencillo este último paso comparado con haber realizado un `git reset` en el caso anterior. Si este último caso fuera en el que me encontrara, hubiera realizado un `git reset --hard HEAD@{1}`, puesto que realmente estoy moviendo el puntero de la rama *master* al commit al que apuntaba antes de moverse al commit inicial.


