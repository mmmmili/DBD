# 📚 Formas Normales en Bases de Datos

Las **formas normales** son reglas que ayudan a diseñar bases de datos bien estructuradas, **evitando redundancia de datos y anomalías** (como duplicaciones o errores al actualizar/eliminar información). Cada forma normal es una mejora de la anterior.

---

## ✅ Primera Forma Normal (1FN)

**Regla:**  
Todos los atributos deben tener **valores atómicos** (una sola cosa, sin listas, sin conjuntos).

**Ejemplo NO válido (violación de 1FN):**
```plaintext
Estudiante(ID, Nombre, Cursos)
(1, Ana, {Matemática, Física}) ❌
```

**Ejemplo correcto en 1FN:**
```plaintext
Estudiante(ID, Nombre, Curso)
(1, Ana, Matemática)
(1, Ana, Física)
```

✔️ Una tabla está en 1FN si:
- No tiene atributos multivaluados ni compuestos.
- Todos los campos contienen datos simples (atómicos).

---

## ✅✅ Segunda Forma Normal (2FN)

**Regla:**  
Estar en **1FN** y que **cada atributo no primo dependa de toda la clave**, no de una parte.

- "Atributo no primo" = no forma parte de una clave candidata  
- "Dependencia parcial" = cuando un atributo depende **de parte** de una clave compuesta

**Ejemplo NO válido en 2FN:**
```plaintext
Inscripcion(EstudianteID, CursoID, NombreEstudiante)
```

- Clave compuesta: (EstudianteID, CursoID)
- NombreEstudiante depende solo de EstudianteID → ❌

**Ejemplo correcto en 2FN:**
```plaintext
Estudiante(EstudianteID, NombreEstudiante)
Inscripcion(EstudianteID, CursoID)
```

---

## ✅✅✅ Tercera Forma Normal (3FN)

**Regla:**  
Estar en **2FN** y que **no haya dependencias transitivas** desde la clave hacia un atributo no primo.

- "Dependencia transitiva" = A → B y B → C, entonces A → C  
(Si C es un atributo no primo → violación de 3FN)

**Ejemplo NO válido en 3FN:**
```plaintext
Empleado(ID, Nombre, DepartamentoID, NombreDepartamento)
```

- ID → DepartamentoID  
- DepartamentoID → NombreDepartamento  
➡️ ID → NombreDepartamento por transitiva ❌

**Ejemplo correcto en 3FN:**
```plaintext
Empleado(ID, Nombre, DepartamentoID)
Departamento(DepartamentoID, NombreDepartamento)
```

---

## 🌟 Forma Normal de Boyce-Codd (BCNF)

**Regla:**  
Para toda dependencia funcional X → Y, **X debe ser una superclave**.

**Ejemplo (está en 3FN pero no en BCNF):**
```plaintext
Curso(Profesor, Aula, Horario)
```

- Supongamos: Profesor → Aula  
- Pero Profesor **no es** superclave → ❌ no cumple BCNF

---

## 🧠 Resumen de Formas Normales

| Forma Normal | Qué evita                    | Requisitos                            |
|--------------|------------------------------|----------------------------------------|
| **1FN**      | Datos repetidos en una celda | Atributos atómicos                     |
| **2FN**      | Dependencias parciales       | En 1FN + sin dependencias parciales    |
| **3FN**      | Dependencias transitivas     | En 2FN + sin transitivas               |
| **BCNF**     | Atributos que no dependen de una superclave | En 3FN + toda X en X→Y es superclave |




