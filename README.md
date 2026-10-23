# Flask: migraciones y ventas

Proyecto de práctica con Flask, Flask-SQLAlchemy, Flask-Migrate/Alembic y SQLite. Incluye modelos de usuarios, clientes, productos, ventas y detalles de venta.

## Requisitos

- Python 3.12 o superior
- Windows, PowerShell o CMD

## Preparar y ejecutar

Desde la carpeta del proyecto:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
flask db upgrade
python seed.py
```

Si PowerShell bloquea la activación, puedes usar CMD:

```cmd
.venv\Scripts\activate.bat
```

La base `bd_ventas.db` se crea en la carpeta del proyecto cuando se aplican las migraciones. `seed.py` agrega datos de demostración y evita duplicarlos si detecta que ya existe un usuario.

## Revisar migraciones

```powershell
flask db current
flask db history
```

Las migraciones crean primero usuarios, clientes y productos; luego ventas y detalles; y finalmente agregan la categoría de producto.

## Comprobar relaciones y total de una venta

```powershell
flask shell
```

En la consola de Flask:

```python
ana = Cliente.query.filter_by(nombre="Ana Pérez").first()
ana.ventas[0].total
[(detalle.producto.descripcion, detalle.cantidad) for detalle in ana.ventas[0].detalles]
```

El total esperado para la primera venta de Ana es `81.50`.

## Datos de demostración

`seed.py` contiene usuarios y contraseñas únicamente para esta práctica local. No reutilices esas credenciales ni las uses en producción.

## Archivos locales excluidos de Git

El entorno virtual y las bases SQLite (`*.db`) son locales; se excluyen del repositorio. En otra computadora, instala los requisitos, ejecuta `flask db upgrade` y después `python seed.py` para reconstruir la base de prueba.
