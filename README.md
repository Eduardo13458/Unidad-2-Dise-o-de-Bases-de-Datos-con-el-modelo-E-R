# Unidad-2-Dise-o-de-Bases-de-Datos-con-el-modelo-E-R
Unidad 2 
[reporte_tecnico_modelado_bd_clinica-v.1Revision.md](https://github.com/user-attachments/files/34098192/reporte_tecnico_modelado_bd_clinica-v.1Revision.md)
**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 1** 



<!-- Start of picture text -->
=aN<br>—— ><br>TECNOLOGICO<br>NACIONAL DE MEXICO<br><!-- End of picture text -->

### **LICENCIATURA EN INFORMÁTICA** 

# **REPORTE TÉCNICO: MODELADO CONCEPTUAL E-R Y E-R EXTENDIDO** 

**Asignatura:** Sistemas de Bases de Datos **Docente** : Ruben Miguel Riojas Rodríguez **Alumno:** Eduardo Salazar Martínez **Fecha de Entrega:** 27 de octubre de 2026 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 2** 

# **REPORTE TÉCNICO: MODELADO CONCEPTUAL** 

## **1. Planteamiento del Problema y Descripción Contextual** 

La institución médica **'Salud Total'** es un centro de atención ambulatoria y especializada que enfrenta ineficiencias operativas debido a la fragmentación de sus registros clínicos y administrativos. La coexistencia de expedientes físicos y hojas de cálculo independientes genera duplicidad de registros, dificultad para rastrear el historial de consultas de los pacientes, traslape en la agenda de citas de los médicos y falta de control estricto sobre los medicamentos prescritos. 

Para resolver esta problemática, se diseñó un modelo de base de datos relacional centralizado fundamentado en el **Modelo Entidad-Relación Extendido (EER)** . Este diseño permite consolidar la información de pacientes, personal médico, departamentos, agendas de citas, diagnósticos de consulta y emisión de recetas en un esquema estructurado que garantiza la integridad referencial, elimina redundancias y optimiza la toma de decisiones operativas. 

## **2. Reglas de Negocio Formales (RN)** 

- **RN-01 (Jerarquía de Personas):** Toda persona registrada en el sistema es clasificada de forma obligatoria y disjunta como Paciente o Médico. Cada persona posee un identificador único (ID_Persona), nombre completo, dirección de residencia, fecha de nacimiento y uno o más teléfonos de contacto. 

- **RN-02 (Expedientes de Pacientes):** Cada paciente cuenta con un número de expediente único y su tipo de sangre. La edad del paciente se calcula dinámicamente a partir de su fecha de nacimiento. 

- **RN-03 (Acreditación Médica):** Cada médico posee una cédula profesional única, fecha de contratación y puede acreditar una o varias especialidades médicas. 

- **RN-04 (Estructura Departamental):** La clínica se organiza en departamentos médicos. Un departamento alberga uno o varios médicos; cada médico pertenece obligatoriamente a un único departamento. 

- **RN-05 (Programación de Citas):** Un paciente puede solicitar múltiples citas a lo largo del tiempo, y un médico atiende múltiples citas. Cada cita almacena un folio único, fecha, hora y estado (Programada, Completada, Cancelada). 

- **RN-06 (Agregación - Consulta Médica):** La atención efectiva derivada de una cita entre un paciente y un médico constituye la Consulta Médica, de la cual se registra el diagnóstico y costo base. 

- **RN-07 (Emisión de Recetas):** A partir de una consulta médica se emite una o más recetas médicas identificadas por folio de receta y fecha de emisión. 

- **RN-08 (Prescripción de Medicamentos):** Una receta incluye uno o varios medicamentos. Para cada medicamento recetado se especifican dosis, frecuencia y duración en días del tratamiento. 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 3** 

## **3. Identificación de Componentes del Modelo E-R** 

|**Entidad**|**Clave Primaria**<br>**(PK)**|**Atributos Simples**|**Atributo Compuesto**|**Atributo**<br>**Derivado**|**Atributo**<br>**Multivalorado**|
|---|---|---|---|---|---|
|Persona (Super)|ID_Persona|Fecha_Nacimiento|Nombre_Completo,<br>Dirección|Edad (calculado)|Teléfono|
|Paciente (Sub)|Num_Expediente|Tipo_Sangre|Heredados de Persona|Heredados de<br>Persona|Heredados de<br>Persona|
|Médico (Sub)|Num_Cédula|Fecha_Contratación|Heredados de Persona|Heredados de<br>Persona|Especialidad|
|Departamento|ID_Depto|Nombre_Depto, Ubicación|N/A|N/A|N/A|
|Cita|Folio_Cita|Fecha, Hora, Estado|N/A|N/A|N/A|
|Consulta|ID_Consulta|Diagnóstico, Costo_Base|N/A|N/A|N/A|
|Receta|Folio_Receta|Fecha_Emisión|N/A|N/A|N/A|
|Medicamento|Código_Med|Nombre_Comercial, Fórmula|N/A|N/A|N/A|



## **4. Aplicación del Modelo E-R Extendido (EER)** 

**A. Jerarquía de Especialización / Generalización:** Se definió la superclase PERSONA y las subclases PACIENTE y MÉDICO. Se aplica una restricción de **Disyunción (d)** porque una instancia no puede ser médico y paciente al mismo tiempo, y una restricción de **Completitud Total (t)** ya que toda persona debe pertenecer obligatoriamente a una de las dos subclases. 

**B. Abstracción por Agregación:** La relación entre PACIENTE, MÉDICO y CITA genera el hecho abstracto CONSULTA MÉDICA, conectando directamente la atención con la emisión de RECETAS mediante la relación (1:N) Prescribe, evitando relaciones ternarias complejas. 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 4** 

## **5. Diagramas Formales del Modelo E-R y EER** 

**Figura 1.** Diagrama Entidad-Relación Completo del Sistema Clínica Salud Total. 



<!-- Start of picture text -->
DIAGRAMA CONCEPTUAL ENTIDAD-RELACION COMPLETO (E-R)<br>Ctinice Salud Total -Modelo de Datos<br>= =<br>eater >> <ntinte ><br>< enim > Cereserta)> Centura ><br>p=kK > =~ kK >| =- kK > —— |<br>(SSE Ea)<br><!-- End of picture text -->

**Figura 2.** Detalle del Modelo E-R Extendido: Jerarquía Persona y Agregación Consulta. 



<!-- Start of picture text -->
DETALLE EER: ESPECIALIZACION Y AGREGACION<br>De: )«|6( nnn<br>H Especializacién Disjunta y Total (d, t) 1 4 Abstraccién por Agregacién (CONSULTA) H<br>' Hin1 1 H q H<br>H hot F 4<br>H | ee | 1 ot CONSULTA MEDICA (Agregacisn) pt<br>H fot ia<br>i +. | ie pot<br>1 (ess) 1;i so: i PACIENTE. FfPoa7<br>H hot F 4<br>H [| l=) 1i '| e 1<br>i_<br>'i 1 1 q<br>SESE SUScUSESECnOEEREORSEESRUGEEEEONnESenecE!1 «© iOCCU UES EEC Ni is emensnnesemeLccusouuensonecaee! q<br><!-- End of picture text -->

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 5** 

## **6. Diccionario de Datos Completo del Sistema** 

El diccionario de datos especifica la estructura física, tipos de datos, longitudes, restricciones de integridad y descripción semántica de las tablas derivadas del modelo relacional: 

**Tabla 1: PERSONA (Superclase de Entidad)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|ID_Persona|INT|4 bytes|NO|PK|AUTO_INCREMENT > 0|Identificador único de la<br>persona.|
|Primer_Nombre|VARCHAR|50|NO|Ninguna|Sin números ni símbolos|Primer nombre de la<br>persona.|
|Apellido_Paterno|VARCHAR|50|NO|Ninguna|Texto alfabético|Primer apellido de la<br>persona.|
|Apellido_Materno|VARCHAR|50|SÍ|Ninguna|Texto alfabético|Segundo apellido de la<br>persona.|
|Calle|VARCHAR|100|NO|Ninguna|Dirección física|Nombre de la calle de<br>residencia.|
|Numero|VARCHAR|20|NO|Ninguna|Alfanumérico|Número exterior e interior.|
|Colonia|VARCHAR|100|NO|Ninguna|Texto|Colonia o fraccionamiento.|
|Codigo_Postal|VARCHAR|10|NO|Ninguna|Formato postal local|Código postal de<br>residencia.|
|Fecha_Nacimiento|DATE|3 bytes|NO|Ninguna|CHECK (Fecha < Actual)|Fecha de nacimiento.|
|Edad_Derivado|INT|4 bytes|SÍ|Derivado|Calculado dinámicamente|Edad en años a la fecha<br>actual.|



**Tabla 2: PERSONA_TELEFONO (Atributo Multivalorado)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|ID_Persona|INT|4 bytes|NO|PK / FK|FK -><br>PERSONA(ID_Persona)|Identificador de la<br>persona.|
|Telefono|VARCHAR|15|NO|PK|Dígitos de contacto|Número telefónico de<br>contacto.|
|**Tabla 3: PACIE**<br>**Nombre Campo**|**NTE (Subcla**<br>**Tipo Dato**|**se de PE**<br>**Longitud**|**RSONA)**<br>**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|Num_Expediente|VARCHAR|20|NO|PK|Formato 'EXP-YYYY-XXXX'|Número único de<br>expediente clínico.|
|ID_Persona|INT|4 bytes|NO|FK / UNQ|FK -><br>PERSONA(ID_Persona)|Vínculo con la superclase<br>persona.|
|Tipo_Sangre|VARCHAR|5|NO|Ninguna|CHECK in<br>('A+','A-','O+','O-',...)|Grupo sanguíneo y factor<br>Rh.|



**Tabla 3: PACIENTE (Subclase de PERSONA)** 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 6** 

**Tabla 4: MEDICO (Subclase de PERSONA)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Num_Cedula|VARCHAR|20|NO|PK|Cédula profesional|Cédula profesional del<br>médico.|
|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|ID_Persona|INT|4 bytes|NO|FK / UNQ|FK -><br>PERSONA(ID_Persona)|Vínculo con la superclase<br>persona.|
|Fecha_Contratacion|DATE|3 bytes|NO|Ninguna|CHECK (Fecha <= Actual)|Fecha de ingreso a la<br>clínica.|
|ID_Depto|INT|4 bytes|NO|FK|FK -> DEPARTAMENTO(ID_<br>Depto)|Departamento al que<br>pertenece.|



**Tabla 5: MEDICO_ESPECIALIDAD (Atributo Multivalorado)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Num_Cedula|VARCHAR|20|NO|PK / FK|FK -><br>MEDICO(Num_Cedula)|Cédula profesional del<br>médico.|
|Especialidad|VARCHAR|50|NO|PK|Texto académico|Nombre de la especialidad<br>acreditada.|



**Tabla 6: DEPARTAMENTO** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|ID_Depto|INT|4 bytes|NO|PK|AUTO_INCREMENT|Identificador del<br>departamento.|
|Nombre_Depto|VARCHAR|100|NO|UNIQUE|Texto único|Nombre del departamento<br>clínico.|
|Ubicacion|VARCHAR|100|SÍ|Ninguna|Texto libre|Piso o ala dentro de la<br>clínica.|



**Tabla 7: CITA** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Folio_Cita|INT|4 bytes|NO|PK|AUTO_INCREMENT|Folio único de la cita<br>médica.|
|Fecha|DATE|3 bytes|NO|Ninguna|Fecha programada|Día asignado para la<br>consulta.|
|Hora|TIME|3 bytes|NO|Ninguna|Horario laboral|Hora programada para la<br>cita.|
|Estado|VARCHAR|20|NO|Ninguna|DEFAULT 'Programada'|Estado (Programada/Com<br>pletada/Cancelada).|
|Num_Expediente|VARCHAR|20|NO|FK|FK -> PACIENTE(Num_Expe<br>diente)|Paciente que solicita la<br>cita.|
|Num_Cedula|VARCHAR|20|NO|FK|FK -><br>MEDICO(Num_Cedula)|Médico asignado para la<br>cita.|



Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 7** 

**Tabla 8: CONSULTA (Agregación)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|ID_Consulta|INT|4 bytes|NO|PK|AUTO_INCREMENT|Identificador de la<br>consulta médica.|
|Folio_Cita|INT|4 bytes|NO|FK / UNQ|FK -> CITA(Folio_Cita)|Cita que origina la<br>consulta.|
|Diagnostico|TEXT|Variable|NO|Ninguna|Min. 10 caracteres|Diagnóstico clínico<br>detallado.|
|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|Costo_Base|DECIMAL|10,2|NO|Ninguna|CHECK (Costo_Base >= 0)|Costo financiero de la<br>consulta.|



#### **Tabla 9: RECETA** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Folio_Receta|INT|4 bytes|NO|PK|AUTO_INCREMENT|Folio único de la receta<br>médica.|
|ID_Consulta|INT|4 bytes|NO|FK|FK -><br>CONSULTA(ID_Consulta)|Consulta donde se emite<br>la receta.|
|Fecha_Emision|DATE|3 bytes|NO|Ninguna|DEFAULT CURRENT_DATE|Fecha de emisión de la<br>receta.|



#### **Tabla 10: MEDICAMENTO** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Codigo_Med|INT|4 bytes|NO|PK|AUTO_INCREMENT|Código interno del<br>medicamento.|
|Nombre_Comercial|VARCHAR|100|NO|Ninguna|Texto comercial|Nombre de marca del<br>medicamento.|
|Formula|VARCHAR|200|NO|Ninguna|Sustancia activa|Composición química o<br>fórmula.|



**Tabla 11: RECETA_MEDICAMENTO (Relación M:N)** 

|**Nombre Campo**|**Tipo Dato**|**Longitud**|**Nulo**|**Clave**|**Restricciones / Default**|**Descripción Semántica**|
|---|---|---|---|---|---|---|
|Folio_Receta|INT|4 bytes|NO|PK / FK|FK -><br>RECETA(Folio_Receta)|Receta que incluye el<br>medicamento.|
|Codigo_Med|INT|4 bytes|NO|PK / FK|FK -> MEDICAMENTO(Codi<br>go_Med)|Medicamento prescrito.|
|Dosis|VARCHAR|100|NO|Ninguna|Ej. '500 mg'|Cantidad por toma<br>prescrita.|
|Frecuencia|VARCHAR|100|NO|Ninguna|Ej. 'Cada 8 horas'|Intervalo de<br>administración.|
|Duracion_Dias|INT|4 bytes|NO|Ninguna|CHECK (Duracion_Dias > 0)|Días totales del<br>tratamiento.|



Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 8** 

## **7. Justificación Técnica del Diseño** 

El diseño del modelo conceptual y diccionario de datos responde a criterios estrictos de ingeniería de bases de datos: 1. **Normalización Inicial (1FN):** Los atributos multivalorados (Teléfonos y Especialidades) se descompusieron en tablas satélite subordinadas, eliminando grupos repetitivos dentro de las entidades principales. 

2. **Mantenibilidad de la Jerarquía:** La especialización de Persona consolida atributos comunes en una sola entidad, evitando duplicar nombres y direcciones en tablas independientes para médicos y pacientes. 

3. **Integridad de Prescripción:** La abstracción de Consulta mediante agregación garantiza que las recetas se emitan únicamente en el marco de una atención médica confirmada, asegurando trazabilidad legal y clínica. 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

**CLÍNICA SALUD TOTAL - REPORTE TÉCNICO E-R / EER** 

**PÁGINA 9** 

## **8. Referencias Bibliográficas (Formato APA 7.ª Edición)** 

- **Coronel, C., & Morris, S.** (2019). _Database Systems: Design, Implementation, & Management_ (13th ed.). Cengage Learning. 

- **Date, C. J.** (2004). _An Introduction to Database Systems_ (8th ed.). Pearson Addison-Wesley. 

- **Elmasri, R., & Navathe, S. B.** (2017). _Fundamentos de sistemas de bases de datos_ (7.ª ed.). Pearson Educación. 

- **Object Management Group.** (2017). _Unified Modeling Language (UML) Specification_ (Version 2.5.1). OMG. 

- **Silberschatz, A., Korth, H. F., & Sudarshan, S.** (2014). _Fundamentos de bases de datos_ (6.ª ed.). McGraw-Hill Education. 

Materia: Bases de Datos | Unidad 2 

Documentación Técnica de Ingeniería 

```mermaid
erDiagram
    PERSONA ||--o{ TELEFONO : "posee (multivalorado)"
    PERSONA {
        int ID_Persona PK
        string Primer_Nombre
        string Apellido_Paterno
        string Apellido_Materno
        string Calle
        string Numero
        string Colonia
        string Codigo_Postal
        date Fecha_Nacimiento
        int Edad_Derivado
    }

    PERSONA ||--|| PACIENTE : "es (EER: Total, Disjunta)"
    PACIENTE {
        string Num_Expediente PK
        string Tipo_Sangre
    }

    PERSONA ||--|| MEDICO : "es (EER: Total, Disjunta)"
    MEDICO ||--o{ ESPECIALIDAD : "acredita (multivalorado)"
    MEDICO {
        string Num_Cedula PK
        date Fecha_Contratacion
    }

    DEPARTAMENTO ||--|{ MEDICO : "alberga (1:N)"
    DEPARTAMENTO {
        int ID_Depto PK
        string Nombre_Depto
    }

    PACIENTE ||--o{ CITA : "solicita (1:N)"
    MEDICO ||--o{ CITA : "atiende (1:N)"
    CITA {
        int Folio_Cita PK
        date Fecha
        time Hora
        string Estado
    }

    CITA ||--o{ RECETA : "genera [CONSULTA] (1:N)"
    RECETA {
        int Folio_Receta PK
        date Fecha_Emision
    }

    RECETA ||--|{ RECETA_MEDICAMENTO : "incluye (M:N)"
    MEDICAMENTO ||--o{ RECETA_MEDICAMENTO : "aparece_en (M:N)"
    MEDICAMENTO {
        int Codigo_Med PK
        string Nombre_Comercial
        string Formula
    }

    RECETA_MEDICAMENTO {
        string Dosis
        string Frecuencia
        string Duracion_Dias
    }
```


TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 



<!-- Start of picture text -->
=aN<br>—— ><br>TECNOLOGICO<br>NACIONAL DE MEXICO<br><!-- End of picture text -->

### **LICENCIATURA EN INFORMÁTICA** 

# **TAREA 2.2: TRANSICION DE DIAGRAMA ENTIDADRELACION A NOTACION UML** 

**Asignatura:** Sistemas de Bases de Datos 

**Docente** : Ruben Miguel Riojas Rodríguez **Alumno:** Eduardo Salazar Martínez 

Pagina 1 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **Contenido** 

|1. Planteamiento del Problema y Contextualizaciones .................................................................. 3|
|---|
|2. Matriz de Correspondencia Directa (E-R a Notacion UML) ....................................................... 3|
|3. Especificación Detallada de Clases y Visibilidad ....................................................................... 4|
|4. Diagrama de Clases UML 2.5 Formal ........................................................................................ 6|
|5. Codigo Fuente Mermaid para Herramienta CASE..................................................................... 7|
|6. Justificacion Tecnica de las Decisiones de Diseño ................................................................... 9|
|7. Referencias Bibliograficas (APA 7a ed.) .................................................................................. 10|



Pagina 2 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **1. Planteamiento del Problema y Contextualizaciones** 

La clínica médica **Salud Total** requiere la transición de su modelo conceptual Entidad-Relación Extendido (EER) hacia una arquitectura orientada a objetos expresada en el Lenguaje de Modelado Unificado (UML 2.5). Esta evolución permite al equipo de ingeniería de software acoplar el diseño de la base de datos con la capa de lógica de negocio en lenguajes como Java o C#, garantizando el encapsulamiento de datos, la reutilización de código mediante herencia y la definición de métodos operativos. 

## **2. Matriz de Correspondencia Directa (E-R a Notacion UML)** 

La siguiente tabla establece la equivalencia semántica y sintáctica entre los componentes del Modelo Entidad-Relación y el Diagrama de Clases UML: 

|**Concepto E-R / EER**|**Equivalente en UML**|**Aplicacion Practica en el**<br>**Sistema Clinico**|
|---|---|---|
|Entidad Superclase|Clase Abstracta (<<abstract>>)|Clase Persona (no instanciable<br>directamente).|
|Entidad Subclase|Clase Concreta Heredada|Clases Paciente y Medico.|
|Entidades Simples|Clases del Dominio|Departamento, Cita, Consulta, Receta,<br>Medicamento.|
|Atributo Clave (PK)|Atributo Identificador ({PK})|idPersona: int {PK}, numExpediente:<br>String {PK}.|
|Atributo Compuesto|Propiedades Desglosadas|Nombre_Completo -> primerNombre,<br>apellidoPaterno, etc.|
|Atributo Derivado|Operacion / Metodo (+)|Edad -> +calcularEdad(): int.|
|Atributo Multivalorado|Atributo Coleccion (List<T>)|Telefono -> telefonos: List<String>.|
|Especializacion (d, t)|Generalizacion / Herencia (<|--)|Paciente y Medico extienden de<br>Persona.|
|Agregacion E-R|Agregacion Compartida (o--)|Departamento (1) o-- (0..*) Medico.|
|Dependencia Existencial|Composicion Fuerte (*--)|Consulta (1) *-- (0..*) Receta.|
|Relacion M:N con Datos|Clase de Asociacion|RecetaMedicamento (dosis, frecuencia,<br>duracion).|



Pagina 3 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **3. Especificación Detallada de Clases y Visibilidad** 

Cada clase se especifica formalmente con visibilidad privada (-) para atributos y pública (+) para métodos, aplicando el principio de encapsulamiento: 

**Clase: Persona (<<abstract>>)** 

#### **Atributos:** 

- idPersona: int {PK} 

- primerNombre: String 

- apellidoPaterno: String 

- apellidoMaterno: String 

- calle: String 

- numero: String 

- colonia: String 

- codigoPostal: String 

- fechaNacimiento: Date 

- telefonos: List<String> 

#### **Metodos:** 

- + calcularEdad(): int 

- + getNombreCompleto(): String 

#### **Clase: Paciente (Hereda de Persona)** 

#### **Atributos:** 

- numExpediente: String {PK} 

- tipoSangre: String 

#### **Metodos:** 

- + consultarHistorial(): List<Cita> 

**Clase: Medico (Hereda de Persona)** 

#### **Atributos:** 

- numCedula: String {PK} 

- fechaContratacion: Date 

- especialidades: List<String> 

#### **Metodos:** 

- + atenderCita(cita: Cita): Consulta 

**Clase: Departamento** 

#### **Atributos:** 

- idDepto: int {PK} 

- nombreDepto: String - ubicacion: String 

Pagina 4 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

**Clase: Cita** 

#### **Atributos:** 

- folioCita: int {PK} 

- fecha: Date 

- hora: Time 

- estado: String 

#### **Metodos:** 

- + cancelarCita(): void 

#### **Clase: Consulta** 

#### **Atributos:** 

- idConsulta: int {PK} 

- diagnostico: String 

- costoBase: Decimal 

#### **Metodos:** 

- + emitirReceta(): Receta 

**Clase: Receta** 

#### **Atributos:** 

- folioReceta: int {PK} 

- fechaEmision: Date 

**Clase: Medicamento** 

#### **Atributos:** 

- codigoMed: int {PK} 

- nombreComercial: String 

- formula: String 

**Clase: RecetaMedicamento (Clase de Asociacion)** 

#### **Atributos:** 

- dosis: String 

- frecuencia: String 

- duracionDias: int 

Pagina 5 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **4. Diagrama de Clases UML 2.5 Formal** 



<!-- Start of picture text -->
DIAGRAMA DE CLASES UML 2.5 - SISTEMA CLINICA SALUD TOTAL<br>||<br>Pe<br>:<br>nombreConercial: String + eaitictemstal): Comat 1 0..*) . techagmision: Date<br>. |<br><!-- End of picture text -->

_Figura 1: Diagrama de Clases UML del Sistema de Gestión Integral 'Clínica Salud Total'._ 

Pagina 6 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **5. Codigo Fuente Mermaid para Herramienta CASE** 

Para reproducción en herramientas CASE (Mermaid Live Editor, Draw.io o VS Code), se provee el siguiente código fuente ejecutable: 

```
classDiagram
    class Persona {
        <<abstract>>
        -int idPersona
        -String primerNombre
        -String apellidoPaterno
        -String apellidoMaterno
        -String calle
        -String numero
        -String colonia
        -String codigoPostal
        -Date fechaNacimiento
        -List~String~ telefonos
        +calcularEdad() int
        +getNombreCompleto() String
    }
    class Paciente {
        -String numExpediente
        -String tipoSangre
    }
    class Medico {
        -String numCedula
        -Date fechaContratacion
        -List~String~ especialidades
    }
    class Departamento {
        -int idDepto
        -String nombreDepto
        -String ubicacion
    }
    class Cita {
        -int folioCita
        -Date fecha
        -Time hora
        -String estado
    }
    class Consulta {
        -int idConsulta
        -String diagnostico
        -Decimal costoBase
        +emitirReceta() Receta
    }
    class Receta {
        -int folioReceta
        -Date fechaEmision
    }
    class Medicamento {
        -int codigoMed
        -String nombreComercial
        -String formula
    }
    class RecetaMedicamento {
        -String dosis
```

Pagina 7 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

```
        -String frecuencia
        -int duracionDias
    }
    Persona <|-- Paciente : Generalizacion
    Persona <|-- Medico : Generalizacion
    Departamento "1" o-- "0..*" Medico : alberga
    Paciente "1" -- "0..*" Cita : solicita
    Medico "1" -- "0..*" Cita : atiende
    Cita "1" -- "0..1" Consulta : origina
    Consulta "1" *-- "0..*" Receta : prescribe
    Receta "1" -- "1..*" RecetaMedicamento : incluye
    Medicamento "1" -- "0..*" RecetaMedicamento : prescribe_en
```

Pagina 8 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **6. Justificacion Tecnica de las Decisiones de Diseño** 

**Encapsulamiento y Métodos Dinámicos:** El atributo derivado Edad del modelo E-R se convirtió en la función pública +calcularEdad(): int. Esto evita la persistencia estática de datos redundantes y garantiza que la edad se calcule en tiempo de ejecución basándose en la fecha actual. 

**Abstracción mediante Clases Abstractas:** La clase Persona se marcó como <<abstract>> debido a que la regla de negocio RN-01 exige cobertura total e idoneidad estricta: ninguna instancia en el sistema es una 'Persona' genérica, sino concretamente un Paciente o un Medico. 

**Diferenciación entre Agregación y Composición:** Se aplicó Agregación Compartida (o--) entre Departamento y Medico porque un médico preserva su existencia operacional aun si un departamento se reorganiza. Por el contrario, se aplicó Composición Fuerte (*--) entre Consulta y Receta debido a la dependencia de existencia estricta de la orden médica. 

**Atributos Multivalorados como Colecciones:** Teléfono y Especialidades se modelan como listas de cadenas (List<String>), aprovechando las capacidades del paradigma de objetos sin necesidad de tablas auxiliares débiles en la capa lógica de software. 

Pagina 9 

TAREA 2.2: TRANSICION DE DIAGRAMA E-R A NOTACION UML | CLINICA SALUD TOTAL 

## **7. Referencias Bibliograficas (APA 7a ed.)** 

Elmasri, R., & Navathe, S. B. (2017). Fundamentals of database systems (7th ed.). Pearson. 

Object Management Group. (2017). Unified Modeling Language (UML) specification, version 2.5.1. OMG. 

- Pressman, R. S., & Maxim, B. R. (2021). Software engineering: A practitioner's approach (9th ed.). McGrawHill Education. 

- Silberschatz, A., Korth, H. F., & Sudarshan, S. (2020). Database system concepts (7th ed.). McGraw-Hill Education. 

Pagina 10 

```mermaid
classDiagram
    class Persona {
        <<abstract>>
        -int idPersona
        -String primerNombre
        -String apellidoPaterno
        -String apellidoMaterno
        -String calle
        -String numero
        -String colonia
        -String codigoPostal
        -Date fechaNacimiento
        -List~String~ telefonos
        +calcularEdad() int
        +getNombreCompleto() String
    }
    class Paciente {
        -String numExpediente
        -String tipoSangre
    }
    class Medico {
        -String numCedula
        -Date fechaContratacion
        -List~String~ especialidades
    }
    class Departamento {
        -int idDepto
        -String nombreDepto
        -String ubicacion
    }
    class Cita {
        -int folioCita
        -Date fecha
        -Time hora
        -String estado
    }
    class Consulta {
        -int idConsulta
        -String diagnostico
        -Decimal costoBase
        +emitirReceta() Receta
    }
    class Receta {
        -int folioReceta
        -Date fechaEmision
    }
    class Medicamento {
        -int codigoMed
        -String nombreComercial
        -String formula
    }
    class RecetaMedicamento {
        -String dosis
        -String frecuencia
        -int duracionDias
    }
    Persona <|-- Paciente : Generalizacion
    Persona <|-- Medico : Generalizacion
    Departamento "1" o-- "0..*" Medico : alberga
    Paciente "1" -- "0..*" Cita : solicita
    Medico "1" -- "0..*" Cita : atiende
    Cita "1" -- "0..1" Consulta : origina
    Consulta "1" *-- "0..*" Receta : prescribe
    Receta "1" -- "1..*" RecetaMedicamento : incluye
    Medicamento "1" -- "0..*" RecetaMedicamento : prescribe_en

```


[tarea_2_2_transicion_uml-v2.0Revision.md](https://github.com/user-attachments/files/34105725/tarea_2_2_transicion_uml-v2.0Revision.md)

