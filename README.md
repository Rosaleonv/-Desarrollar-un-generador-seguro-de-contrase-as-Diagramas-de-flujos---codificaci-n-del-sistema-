# 🔐 Generador Seguro de Contraseñas

## 📌 Descripción
Proyecto que permite generar contraseñas seguras de manera rápida y confiable. Ofrece distintos niveles de seguridad y copia automáticamente la contraseña al portapapeles, ayudando a proteger la información personal y cuentas digitales.

## ⚙️ Funcionalidades
- **Contraseñas por nivel de seguridad**:
  - **Baja:** simple y corta.
  - **Media:** combinación de letras y números.
  - **Alta:** combinación de letras, números y símbolos.
- Copiado automático al portapapeles.
- Interfaz gráfica amigable desarrollada con **Tkinter**.
- Compatible con Python 3.x.

## 📊 Diagramas de Flujo
- [Diagrama de flujo principal][[(ruta_a_tu_diagrama1.xml)  ](https://github.com/Rosaleonv/-Desarrollar-un-generador-seguro-de-contrase-as-Diagramas-de-flujos---codificaci-n-del-sistema-/blob/main/DIAGRAMAS%20DE%20FLUJO-Casos%20de%20Uso%201.png)](https://github.com/Rosaleonv/-Desarrollar-un-generador-seguro-de-contrase-as-Diagramas-de-flujos---codificaci-n-del-sistema-/blob/main/DIAGRAMAS%20DE%20FLUJO-Casos%20de%20Uso%201.png)
- [Diagrama de generación de contraseñas] https://github.com/Rosaleonv/-Desarrollar-un-generador-seguro-de-contrase-as-Diagramas-de-flujos---codificaci-n-del-sistema-/blob/main/DIAGRAMAS%20DE%20FLUJO-Arquitectura.%202.png 
- [Diagrama de copiado al portapapeles] https://github.com/Rosaleonv/-Desarrollar-un-generador-seguro-de-contrase-as-Diagramas-de-flujos---codificaci-n-del-sistema-/blob/main/DIAGRAMAS%20DE%20FLUJO-P%C3%A1gina-3..png

## 👥 Datos del Grupo
- Rosa León – rosaleonv@example.com  

## 🎯 Objetivo
Proveer una herramienta que permita generar contraseñas seguras de forma fácil y rápida, fortaleciendo la protección de información sensible.

## 📅 Fecha del Proyecto
24 de agosto de 2025

## 💻 Requisitos
- Python 3.x  
- Librerías: `tkinter`, `random`, `pyperclip`  

### Instalación de librerías
```bash
pip install pyperclip

## Codigo Generador de Contraseñas Seguras con Interfaz Gráfica
"""

import tkinter as tk
from tkinter import messagebox
import random
import string
import pyperclip

# --- Función para evaluar la fortaleza ---
def evaluar_fortaleza(contraseña):
    # Calcula la longitud de la contraseña
    longitud = len(contraseña)
    tiene_mayusculas = any(c.isupper() for c in contraseña)
    tiene_minusculas = any(c.islower() for c in contraseña)
    tiene_numeros = any(c.isdigit() for c in contraseña)
    tiene_especiales = any(c in string.punctuation for c in contraseña)

    # Puntaje basado en tipos de caracteres presentes
    puntaje = sum([tiene_mayusculas, tiene_minusculas, tiene_numeros, tiene_especiales])

    if longitud >= 12 and puntaje == 4:
        return "Fuerte", "green"
    elif longitud >= 8 and puntaje >= 3:
        return "Media", "orange"
    else:
        return "Débil", "red"

# --- Generar contraseña ---
def generar_contraseña():
    try:
        longitud = int(entrada_longitud.get())
    except ValueError:
        messagebox.showerror("Error", "Ingresa un número válido para la longitud")
        return

    if longitud < 4:
        messagebox.showerror("Error", "La longitud mínima es 4")
        return

    caracteres = ""
    if var_mayusculas.get():
        caracteres += string.ascii_uppercase
    if var_minusculas.get():
        caracteres += string.ascii_lowercase
    if var_numeros.get():
        caracteres += string.digits
    if var_especiales.get():
        caracteres += string.punctuation

    if not caracteres:
        messagebox.showerror("Error", "Selecciona al menos un tipo de carácter")
        return

    contraseña = "".join(random.choice(caracteres) for _ in range(longitud))
    entrada_resultado.delete(0, tk.END)
    entrada_resultado.insert(0, contraseña)

    # Mostrar fortaleza
    fortaleza, color = evaluar_fortaleza(contraseña)
    etiqueta_fortaleza.config(text=f"Fortaleza: {fortaleza}", fg=color)

# --- Copiar contraseña ---
def copiar_contraseña():
    contraseña = entrada_resultado.get()
    if contraseña:
        pyperclip.copy(contraseña)
        messagebox.showinfo("Copiado", "La contraseña se ha copiado al portapapeles")
    else:
        messagebox.showwarning("Aviso", "No hay contraseña para copiar")

# --- Interfaz ---
ventana = tk.Tk()
ventana.title("Generador de Contraseñas Seguras")
ventana.geometry("400x350")
ventana.resizable(False, False)

# Entrada longitud
tk.Label(ventana, text="Longitud:").pack(pady=5)
entrada_longitud = tk.Entry(ventana, width=10)
entrada_longitud.pack()

# Opciones
var_mayusculas = tk.BooleanVar(value=True)
var_minusculas = tk.BooleanVar(value=True)
var_numeros = tk.BooleanVar(value=True)
var_especiales = tk.BooleanVar(value=True)

tk.Checkbutton(ventana, text="Mayúsculas", variable=var_mayusculas).pack(anchor="w", padx=50)
tk.Checkbutton(ventana, text="Minúsculas", variable=var_minusculas).pack(anchor="w", padx=50)
tk.Checkbutton(ventana, text="Números", variable=var_numeros).pack(anchor="w", padx=50)
tk.Checkbutton(ventana, text="Caracteres especiales", variable=var_especiales).pack(anchor="w", padx=50)

# Botón generar
tk.Button(ventana, text="Generar", command=generar_contraseña).pack(pady=10)

# Resultado
entrada_resultado = tk.Entry(ventana, width=30)
entrada_resultado.pack(pady=5)

# Fortaleza
etiqueta_fortaleza = tk.Label(ventana, text="Fortaleza: ", font=("Arial", 10, "bold"))
etiqueta_fortaleza.pack()

# Botón copiar
tk.Button(ventana, text="Copiar", command=copiar_contraseña).pack(pady=10)

ventana.mainloop()
