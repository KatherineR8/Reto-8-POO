# Reto-8-POO
### Katherine Restrepo
#### Take the Menu code from Reto 3 and implement a new Class that creates and iterable with all the items in an order, it should allow looping and contain all item attributes.
```python
class ElementoMenu:
    def __init__(self, nombre: str, precio: float):
        self.nombre = nombre
        self.precio = precio

    def calcular_precio_total(self):
        return self.precio

    def __str__(self):
        return f"{self.nombre} - ${self.precio:.2f}"

    def __len__(self):
        return 1  # Cada elemento cuenta como 1 unidad


class Bebida(ElementoMenu):
    def __init__(self, nombre, precio, con_azucar: bool = False):
        super().__init__(nombre, precio)
        self.con_azucar = con_azucar


class Entrada(ElementoMenu):
    def __init__(self, nombre, precio, con_sal: bool = False):
        super().__init__(nombre, precio)
        self.con_sal = con_sal


class PlatoPrincipal(ElementoMenu):
    def __init__(self, nombre, precio, vegano: bool = False):
        super().__init__(nombre, precio)
        self.vegano = vegano


class IteradorOrden:
    def __init__(self, items):
        self.items = items
        self.indice = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.indice < len(self.items):
            item = self.items[self.indice]
            self.indice += 1
            return item
        else:
            raise StopIteration


class Orden:
    def __init__(self):
        self.items = []

    def agregar_elemento(self, item: ElementoMenu):
        self.items.append(item)

    def calcular_total(self):
        return sum(item.calcular_precio_total() for item in self.items)

    def aplicar_descuento(self, porcentaje: float):
        total = self.calcular_total()
        return total - (total * porcentaje / 100)

    def __iter__(self):
        return IteradorOrden(self.items)

```
