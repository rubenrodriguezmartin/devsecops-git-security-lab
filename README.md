# devsecops-git-security-lab

Laboratorio académico orientado a la aplicación de controles de seguridad sobre repositorios Git y al estudio de diferentes técnicas de prevención, detección y remediación de secretos.

El proyecto recorre desde la auditoría del historial y la gestión de ramas hasta la implementación de hooks, firma de commits, prevención de credenciales y detección de secretos expuestos mediante herramientas específicas de DevSecOps.

>
> Este repositorio corresponde a un laboratorio académico realizado en un entorno controlado.
> Todas las credenciales, claves, tokens y secretos utilizados durante las pruebas son ficticios o fueron creados exclusivamente con fines formativos.

---

## Objetivos

Los principales objetivos del laboratorio fueron:

- Comprender cómo Git almacena y conserva el historial de cambios.
- Trabajar con flujos de desarrollo basados en ramas mediante GitFlow.
- Automatizar controles mediante Git Hooks.
- Implementar hooks de forma mantenible utilizando Husky.
- Firmar commits mediante GPG para verificar su autoría e integridad.
- Prevenir la inclusión accidental de credenciales en repositorios.
- Detectar secretos presentes en el historial de Git.
- Comprobar que eliminar un fichero no elimina necesariamente su contenido del historial.
- Remediar una exposición mediante reescritura del historial.
- Analizar repositorios remotos en busca de posibles secretos.

---

## Tecnologías y herramientas

- Git
- GitHub
- GitFlow
- Git Hooks
- Husky
- npm
- GPG
- git-secrets
- TruffleHog
- git-filter-repo
- SourceTree

---

## Estructura del laboratorio

| Sección | Contenido | Práctica original |
|---|---|---:|
| [01 - Auditoría del historial de Git](./01-auditoria-historial-git/) | Inspección de commits, diferencias, autoría y evolución del repositorio | 2.2 |
| [02 - Flujo de trabajo con GitFlow](./02-flujo-gitflow/) | Gestión de ramas `develop`, `feature`, `release` y `hotfix` | 2.3 |
| [03 - Hooks nativos de Git](./03-hooks-nativos-git/) | Automatización mediante `pre-commit`, `commit-msg` y otros hooks | 2.4 |
| [04 - Hooks con Husky](./04-hooks-con-husky/) | Gestión automatizada de hooks dentro del proyecto | 2.5 |
| [05 - Firma de commits con GPG](./05-firma-commits-gpg/) | Generación de claves y firma criptográfica de commits | 2.6 |
| [06 - Prevención de secretos con git-secrets](./06-prevencion-secretos-git-secrets/) | Bloqueo preventivo de credenciales y patrones sensibles | 2.7 |
| [07 - Detección y remediación de secretos](./07-deteccion-remediacion-secretos/) | TruffleHog, persistencia de secretos y limpieza del historial | 2.8 |
| [08 - Escaneo remoto de secretos](./08-escaneo-remoto-secretos/) | Análisis de repositorios remotos mediante TruffleHog | 2.9 |

---

## Flujo de seguridad implementado

Una de las partes principales del laboratorio consiste en analizar el ciclo completo que puede seguir una credencial expuesta dentro de un repositorio.

```text
Desarrollador
     │
     ▼
Git Hooks / Husky
     │
     ▼
git-secrets
     │
     ├──── Secreto detectado ────► Commit bloqueado
     │
     ▼
Commit realizado
     │
     ▼
Secreto almacenado en el historial
     │
     ▼
TruffleHog
     │
     ▼
Detección del secreto
     │
     ▼
git-filter-repo
     │
     ▼
Reescritura del historial
     │
     ▼
Nuevo escaneo
     │
     ▼
Repositorio limpio
```
Este ejercicio permite comprobar un concepto especialmente importante en Git:

> Eliminar un fichero que contiene una credencial no significa necesariamente que la credencial haya desaparecido del repositorio, ya que puede continuar almacenada en commits anteriores.

---

## Prevención de secretos

Se utilizó **git-secrets** para definir controles capaces de identificar patrones sensibles antes de que fueran incorporados al historial.

Durante el laboratorio se trabajó con credenciales ficticias y patrones personalizados para comprobar el comportamiento de los controles preventivos.

El objetivo fue reproducir un escenario en el que un desarrollador introduce accidentalmente información sensible y el repositorio impide que llegue a registrarse mediante un commit.

---

## Detección con TruffleHog

También se trabajó desde una perspectiva reactiva.

Se simuló la incorporación de una credencial a un repositorio y posteriormente se eliminó el fichero que la contenía.

Mediante **TruffleHog** se comprobó que el secreto continuaba presente en el historial de Git pese a que ya no existía en la versión actual del proyecto.

Este escenario permitió estudiar la diferencia entre:

- eliminar un fichero del working tree;
- eliminarlo de un commit actual;
- eliminar realmente la información de todo el historial.

---

## Remediación

Una vez identificado el secreto, se utilizó **git-filter-repo** para reescribir el historial y eliminar las referencias afectadas.

Tras el proceso de remediación se realizó un nuevo análisis con TruffleHog para verificar que el secreto ya no aparecía entre los resultados.

De esta forma se trabajó el ciclo completo:

**Prevención → Exposición → Detección → Remediación → Verificación**

---

## Integridad y firma de commits

El laboratorio incluye también la configuración de **GPG** para la firma criptográfica de commits.

El objetivo de esta práctica fue trabajar conceptos relacionados con:

- autenticidad del autor;
- integridad del historial;
- verificación de commits;
- gestión de claves criptográficas asociadas a Git.

---

## Git Hooks y Husky

Se utilizaron primero hooks nativos de Git para comprender su funcionamiento y posteriormente **Husky** para integrarlos de una forma más mantenible dentro del flujo de desarrollo.

Entre los controles estudiados se encuentran hooks ejecutados durante diferentes fases del ciclo de Git, permitiendo automatizar comprobaciones antes o después de determinadas operaciones.

---

## Competencias trabajadas

Este laboratorio me permitió trabajar de forma práctica conocimientos relacionados con:

- DevSecOps
- Seguridad en repositorios Git
- Gestión segura de secretos
- Detección de credenciales expuestas
- Reescritura y auditoría del historial
- Firma criptográfica de commits
- Automatización mediante hooks
- GitFlow
- Troubleshooting
- Documentación técnica

---

## Consideraciones de seguridad

Todo el contenido de este repositorio tiene fines exclusivamente educativos.

Las credenciales utilizadas en los ejercicios son ficticias y no proporcionan acceso a sistemas reales.

Cuando se muestran resultados obtenidos durante el análisis de repositorios externos, cualquier información potencialmente sensible debe aparecer anonimizada u ocultada.

---

## Contexto académico

Laboratorio realizado como parte del **Curso de Especialización en Ciberseguridad en Entornos de las Tecnologías de la Información** del IES Politécnico Jesús Marín.

El repositorio ha sido reorganizado posteriormente con fines de portfolio profesional, manteniendo el contenido técnico desarrollado durante las prácticas.

---

## Autor

**Rubén Rodríguez Martín**

Técnico de Sistemas y Ciberseguridad

- LinkedIn: [Rubén Rodríguez Martín](https://www.linkedin.com/in/ruben-rodriguez-martin/)
- GitHub: [@rubenrodriguezmartin](https://github.com/rubenrodriguezmartin)