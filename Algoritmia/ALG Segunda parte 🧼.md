# 22 Marzo 2022 💈
---
## Programación dinámica
- Tenemos un array donde guardamos resultados intermedios para calcular el resultado final.
- Es un método iterativo, cuyo origen es una función recursiva. Sustituimos las llamadas recursiva por accesos a las posiciones del array.
![[funcion recursiva.png|300]]
- Se repiten operaciones, por tanto se guardan las calculadas en un array para no recalcularlas varias veces.
---
## Problema del cambio
![[problema cambio.jpeg]]
Lo que no se ve son 10 céntimos :-)
- Buscar el mínimo para no pasarse, usando la moneda de la iteración o de iteraciones anteriores.
---
## Backtracking
- **Problema de las 8 reinas:** colocar 8 reinas en un tablero sin que se coman.
- **Backtracking** explora el grafo, va desarrollando estados hasta que encuentra una solución. Es un *algoritmo de fuerza bruta*, puesto que lo que hace es desarrollar estados de forma rápida hasta encontrar una solución.
- Técnica ineficiente, con complejidades exponenciales.
![[recorrido en profundidad.png]]
- **Grafo implícito:** grafo que se desarrolla a medida que se va recorriendo. Ahorra tiempo de ejecución y espacio en memoria.
![[grafo implicito.png]]

#### Esquema Backtracking
```java
 

public static void backtracking(Estado e) {

	if (e.esSolucion()) { System.out.println(e); haySolucion= true;

	}  
	else {

		Estado estadoHijo= null; 
		while(e.hasNextHijos() && !haySolucion) {
		// siguiente estado hijo válido 
			estadoHijo= e.nextHijo(); 
			
			if (estadoHijo!=null) // puede que no queden hijos válidos backtracking(estadoHijo);
		}


} }
```
---
# 29 Marzo 2022 🗿
---
- Backtracking busca todas las soluciones posibles.
- También se puede buscar la solución óptima.
---
## Poda de nodos
- Consiste en establecer una condición que impida seguir desarrollando nodos aunque sean válidos.
- Se aplica cuando tenemos que buscar una solución óptima.
- Backtracking tiene complejidad explonencial.
---
### Ejercicio formar palabras a partir de un conjunto de letras
![[formar palabras planteo.png]]
![[formar palabras.png]]
```java
 public static void backtracking (int nivel) {

	if (nivel==m) //hay ya una palabra completa {

		mostrarSolucion();

		cont++; 
	}

	else  {
		for (int i=0;i<n;i++){

			if (!marca[i]) {

				sol[nivel] =vLetras[i]; 
				marca[i]=true; 
				backtracking(nivel+1); 
				marca[i]=false;
			}
		}
	}

}
```
---
### Problema de la asignación de tareas a agentes
![[tareas agentes.png]]
![[tareas agente res.png]]
```java
 static void backtracking (int nivel) {  
	if (nivel==n) { //hay ya una asignación completa

		if (coste<costeMejor) { 
			for (int k=0;k<n;k++){
				 asigMejor[k]=asig[k];
			costeMejor=coste; 
			}
		} }

	else {  
		for (int i=0;i<n;i++){

			if (!marca[i] && coste<costeMejor ) //ostemMejor->poda
				asig[nivel]=i;
				coste=coste+w[nivel][i]; 
			    marca[i]=true; 
			    backtracking(nivel+1); 
			    coste=coste-w[nivel][i]; 
				marca[i]=false;
		}

	} 
}
```
- Se podría hacer una poda (costemejor).
---
